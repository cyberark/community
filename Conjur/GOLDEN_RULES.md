- [Golden Invariants of Debt-Free Codebases](#golden-invariants-of-debt-free-codebases)
  * [1. Common development tasks must be easy](#1-common-development-tasks-must-be-easy)
  * [2. The CI must be fast](#2-the-ci-must-be-fast)
  * [3. Unit tests must run instantly](#3-unit-tests-must-run-instantly)
  * [4. Tests must be reliable and consistent](#4-tests-must-be-reliable-and-consistent)
  * [5. How things work must be clear](#5-how-things-work-must-be-clear)
  * [6. All dependencies must be explicit](#6-all-dependencies-must-be-explicit)
  * [7. Code cannot break due to outside changes](#7-code-cannot-break-due-to-outside-changes)
  * [8. Best practices must be documented for common tasks](#8-best-practices-must-be-documented-for-common-tasks)
  * [9. New tools require documented public discussion. Avoid unnecessary tools](#9-new-tools-require-documented-public-discussion-avoid-unnecessary-tools)
  * [10. Avoid overengineering: Solve only your immediate problem](#10-avoid-overengineering-solve-only-your-immediate-problem)

# Golden Invariants of Debt-Free Codebases

## 1. Common development tasks must be easy

The specifics here will vary from repo to repo, but usually at minimum this
means:

- Single command to start dev environment
- Option flags for common use cases
- Easily run all (or a subset) of tests locally
- Hot re-loading of changes
    - For example, a manual web server restart should not be required after
      every code change (currently broken in Conjur)
- Debugging instructions should be documented when relevant, so each
  developer won't re-invent this particular wheel.
  [Conjur](https://github.com/cyberark/conjur/blob/master/CONTRIBUTING.md#rubymine-ide-debugging)
  has a good example of this.
- Use a consistent interface across repositories for these tasks (when
  possible)

_Discussion_:

Futzing around with docker and bash scripts just _to get started_ on your
work is a velocity and motivation killer.  It also means less focus on the
actual work that will impact customers.

A repository's dev scripts must be _rock solid_.  They must handle all
typical dev use cases.  They must always be up to date.  Their
documentation must always be correct.

## 2. The CI must be fast

- The goal should be 5 minutes or less.  Anything beyond 10 minutes should
  be considered a bug and addressed immediately.
- This will likely mean splitting off longer running tests into jobs that
  get run nightly or hourly, rather than as part of the standard CI tests.
  
  This, in turn, will mean that long-running tests should be "sanity tests"
  that "everything still works when wired up", and should fail rarely if
  the CI tests pass.
- A related option is for the CI to kick off jobs that don't block merging,
  but would still provide feedback about which (possibly already merged)
  change caused the breakage.

_Discussion_:

Some features cannot be tested locally.  

This means the CI speed is a (sometimes drastic) bottleneck for cycle time.  

That is to say...

![compiling](https://imgs.xkcd.com/comics/compiling.png)

For example, on the Rails 5 upgrade work, there were cases where the tests
passed locally and failed on the CI, forcing us to use the CI as a very slow
debugger.  Also, some pipeline steps -- like submitting code coverage to
CodeClimate -- use CI specific functions.  When there is problem with these,
you must also debug via the CI.  

We should minimize these CI dependencies as much as possible, but having a fast
CI makes dealing with them much easier when they do bite us.

Even when features can be tested locally, a slow CI makes PRs slower.

This happens in two ways:

1. A PR that would have been approved and merged, say, Monday afternoon,
   now has to wait until Tuesday morning.  With morning meetings, that
   becomes Tuesday afternoon, and so on.
2. Compounding effects with parallel work: One dev is done, submits final
   changes, PR is approved.  By the time CI finishes, another dev's work
   was merged.  First devs's branch is now out of date.  First dev has to
   rebase, re-submit, wait for CI again.

   Note: The only problem here is the speed of the CI.  We want to enable
   developers to work in parallel, and we want to rebase before merging.

## 3. Unit tests must run instantly

If unit tests are taking longer than a second to run, they are in all
likelihood not actual unit tests, but integration tests that we are calling
unit tests.

Unit tests:

- Test code logic only.
- Use doubles or mocks for dependencies with side effects.  Therefore, if
  your unit tests are slow, you have probably not isolated your logic, and
  are using a real database or a real network.

## 4. Tests must be reliable and consistent

- Tests cannot flap (randomly fail some percentage of the time).
- Failures give clear and precise error messages.
- The only reasons for a passing test to fail in the absence of code
  changes are hardware or other infrastructure failure.  This should be
  extremely rare.
- A test which fails because of a race condition, timeout, or any other low
  probability event arising from the code itself is a bug and should be
  considered an unacceptable defect.

## 5. How things work must be clear

You can't trust or reliably maintain a system you don't understand.

This point applies to all levels of the system, but especially to the
highest levels:  how the CI pipeline works;  how code flows from the
entrypoint down through its components; and how end to end tests work.

Proposed high level rules here:

- No overly complex tests
    - Tests with too much setup code
    - Tests with too many or too deeply nested mocks
    - Specifics on tooling, test libraries, and how to use them TBD via
      public discussion and code reviews.  Secretless is a good example of
      a repo that has simple, effective guidelines around testing.
- No complex test runners (e.g., Conjur's current `ci/test` script is
  unacceptably bloated and complex)
- Architecture is simple and documented (needs elaboration)
- Names of methods, classes, and variables are clear and accurate.
- Context that can't be expressed in code is captured is comments: If you
  spend time figuring something out, make it clear for the next developer.

## 6. All dependencies must be explicit

This is related to the previous point.

Implicit dependencies come in _many_ forms, and might be the single greatest
enemy of maintainable code, because they make it impossible to reason using
only local context.  They neuter our best weapon in the fight against
complexity: the ability to decompose a big problem into small, independent
parts.

Here are some common types of implicit dependencies in our projects:

- In ruby: dependencies from controller inheritance and mixins (often Rails
  "concerns")
- Hidden dependencies on environment variables
- Convoluted dependencies on state in end to end tests (via cucumber's
  "world" object)
- Assumptions about functions provided by the CI environment.  Lack of
  versioning of these functions compounds this.

## 7. Code cannot break due to outside changes

This is the great "pinning" question, and is related to the rule "Tests must
be reliable and consistent"

Proposed invariant: 

**A commit passing CI tests should never break if the code has not changed.**

This indicates a hidden dependency that should be removed.

Strategies for achieving this:

- Pinning
- Explict upgrades that occur in their own commit (of gems/modules,
  language version, OS version, anything else relevant)

To emphasize:

- Breakage without code change should _never_ happen.  If it does, it
  should be treated as seriously as finding a security bug.
- Said another way: Builds and tests should behave identically regardless
  of time and machine spec.
  

_Discussion:_

We don't want to lose security updates to achieve this.  We want a solution
that both maintains this invariant and allows or enforces frequent security
updates, works with vulnerability scanners, and so on.  All of these could
be enforced at the CI level without giving up pinning.

## 8. Best practices must be documented for common tasks

We currently lack unambiguous guidelines for many tasks that could have
them.

This leads to:

- Wasted time reinventing the wheel
- Inconsistency
- Suboptimal solutions
- Wasted time reading code: The reader must understand every different
  solution to a problem, rather than a single canonical one.

_Discussion:_

While not everything can be standardized, much can.  There is a spectrum as
well: From the cut and dried (style and linting decisions) to the more
abstract (code organization).

One place where standarization would help a lot is best practices for testing.
We should have clear guidelines around:

- When unit tests should be used
- How they should be written, and what tools should be used to write them.
- When end to end tests should be used
- How they should be written, and what tools should be used to write them.
- How extensive each type of test should be, depending on context

Of course, developer judgement won't be mechanized away here by any stretch.
But we can still significantly improve quality and consistency with good
guidelines.

## 9. New tools require documented public discussion. Avoid unnecessary tools

Tools are much, much costlier than they first appear.

- Prefer simple and well-known solutions.
- Prefer the standard library to third party solutions.
- Even junior developers should be able to understand our code easily.
- If you think a new tool _is_ justified, raise it publicly.
 
  If other developers agree, document the decision and the reasons for
  making it in the `README.md`, a `DESIGN.md`, a `TOOL.md` or another
  canonical location (TBD).

Adding new technology -- whether in the form of a new language, a new ruby
gem, a new Go module, or anything else -- should be considered a serious
decision with long-term consequences, typically lasting for years.

Every new tool...

- Must be learned by every current and future developer.  

  This has both a time cost and a _risk_ cost:  
  **Less expertise = more likely mistakes.**
- Must be upgraded and maintained.

  As we saw in both the Rails 5 upgrade and the Conjur UI upgrade, fixing
  breaking changes in dependency updates can be a significant time sink.
- Is usually an _implicit_ dependency of every project.

   This makes it easy to "fool yourself" about the true cost, since it
   remains invisible.

   We should make it _explicit_, and maintain a list of all langauges and
   tools a Conjur developer is expected to know, and the degree of expected
   expertise (TBD: per project lists may make more sense than a global
   one).

  Currently my guess at the global list is:
    - Ruby (high)
    - Go (high)
    - Bash (high)
    - Docker (mid)
    - Docker Compose (mid)
    - Kubernetes (?)
    - OpenShift (?)
    - Others?

_Discussion:_

An honest assessment of the disparity between the overall required
expertise to work effectively with our systems and the _average actual
expertise_ should strongly inform decisions to add new tools and languages.  
    
**This disparity is a powerful hidden form of technical debt**

- References:
    - ["Choose Boring
      Technology"](https://mcfunley.com/choose-boring-technology)

## 10. Avoid overengineering: Solve only your immediate problem

> We can solve any problem by introducing an extra level of indirection...
> except for the problem of too many levels of indirection.

  <cite>--[Fundamental theorem of software engineering](https://en.wikipedia.org/wiki/Fundamental_theorem_of_software_engineering)</cite>

This rule is more open to interpretation than some of the others, but there
will be cases where a violation is unambiguous, and it remains a useful
ideal.

- Don't create abstractions in anticipation of future requirements.
- Instead, solve the immediate problem with the least amount of abstraction
possible. 
- When the future requirement becomes an _actual_ requirement... that is
  the time to refactor and introduce your abstraction.

# Next steps

Given the above, where should our first cleanup efforts be?  Initial efforts
should lower risk and maximize immediate value.  Speeding up the Conjur CI
pipeline might be a good place to start.
