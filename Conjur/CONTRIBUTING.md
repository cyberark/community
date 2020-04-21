# Contributing to the Conjur Open Source Projects

Thanks for your interest in Conjur Open Source!

This document serves as a general guide for how to get started as a contributor. If you have any
questions, please ask us on [Discourse](https://discuss.cyberarkcommons.org)!

# Table of Contents

* [Before You Get Started](#before-you-get-started)
  + [Review the contributor license agreements](#review-the-contributor-license-agreements)
  + [Read the Code of Conduct](#read-the-code-of-conduct)
* [Start Contributing](#start-contributing)
  + [Reporting an Issue](#reporting-an-issue)
  + [Contributing to Code](#contributing-to-code)
    - [Find Something to Work On](#find-something-to-work-on)
    - [Working on Issues](#working-on-issues)
    - [Submitting Pull Requests](#submitting-pull-requests)
* [Release Process](#release-process)
* [Appendix](#appendix)
  * [Git Workflow Guidelines](#git-workflow-guidelines)
  * [Changelog Guidelines](#changelog-guidelines)
    + [Changelog Format](#changelog-format)
    + [Changelog Content](#changelog-content)
  * [Tagging](#tagging)
  * [GitHub Releases](#github-releases)
    + [Draft Release Creation](#draft-release-creation)
    + [Pre-release Publishing](#pre-release-publishing)
    + [Release Publishing](#release-publishing)
  * [Open Source Guidelines](#open-source-guidelines)
    + [When the Repo Includes the CLA](#when-the-repo-includes-the-cla)
    + [When the Repo Does Not Include the CLA](#when-the-repo-does-not-include-the-cla)
      - [Signing Off a Commit](#signing-off-a-commit)
      - [Verifying That You Have Signed a Commit](#verifying-that-you-have-signed-a-commit)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with
markdown-toc</a></i></small>


## Before You Get Started

### Review the contributor license agreements

Before your code can be approved, please read our [CLA guide](#open-source-guidelines) to ensure
you're compliant with our contributor license agreements, which includes instructions for:

- [When the Repo Includes the CLA](#when-the-repo-includes-the-cla)
- [When the Repo Does Not Include the CLA](#when-the-repo-does-not-include-the-cla)

### Read the Code of Conduct
Please familiarize yourself with our [Code of Conduct](CODE_OF_CONDUCT.md), which details our
community guidelines and provides instructions for how to get in touch to report violations.

## Start Contributing

### Reporting an Issue

An important part of contributing is adding your experience and perspective to the conversation.
Maybe you've found an issue, or have additional information for an existing issue. In either case,
your voice matters, and we always value your input.

Please read our general guidelines on [reporting an issue](/CONTRIBUTING.md#reporting-an-issue) for
more information

### Contributing to Code

#### Find Something to Work On

1. Check out [our projects](cyberark.github.io/conjur) to find more information about the tools and
   integrations we're building, and pick one that interests you.

1. [Choose an issue](/CONTRIBUTING.md#finding-issues-to-work-on) in that project.

1. Locate the project's CONTRIBUTING.md file, which documents contribution guidelines and in
   particular details the steps required to run, build, and test the project. There are usually
   development prerequisites in these guides that are important for getting set up. Can't find a
   project's CONTRIBUTING.md? Please create an issue or submit a PR to create one!

#### Working on Issues

> Note: In addition to understanding the high-level workflow for issues, it is important to review
> our [Git Development Workflow](#git-workflow-guidelines) first, for following best-practices while
> using source control.

Now that you've chosen a project and an issue and have familiarized yourself with the
project-specific contribution guide, you're ready to start contributing! If you're not sure which
steps to take to get a local copy of the code and start working, you can refer to our general
guidelines for [working on an issue](/CONTRIBUTING.md#working-on-issues) for guidance.

Make sure to update the [CHANGELOG.md](CHANGELOG.md) with any notable changes you may have
before opening a pull request. You can use our [Changelog Guidelines](#changelog-guidelines)
to learn about how to maintain this file.

#### Submitting Pull Requests

Once you've completed the work to resolve the issue and ensured your changes are tested
appropriately, it's time to submit your changes for review. Find out more about submitting your PRs
and getting them merged in our [code review guidelines](/CONTRIBUTING.md#code-reviews).

## Release Process

Our release process generally follows this pattern for most projects:

1. The maintainers agree that a release should be made from current work on default branch. This
   may include 1 or more individuals and can include input from project management, product
   management, technical writers, infrastructure, etc.
2. [**Annotated** git tag is created](#tagging).
3. [Draft release is created](#draft-release-creation) from that tag.
4. After some local smoke testing, a [pre-release is published](#pre-release-publishing).
5. Finally, after some project-dependent amount of user testing, the pre-release is then
   [published as a regular release](#release-publishing).
6. (optional) For some components, a bigger suite release is done when enough projects reach a
   agreed-upon threshold of features that have been tested together.

## Appendix

## Git Workflow Guidelines

The following guidelines are used to maintain a clean and consistent source control history, and are
important to follow when developing.

- Avoid branching off of branches.
    + Branching off of branches can muddle your git history, or make things harder to track and
      maintain when the parent branch changes.
    + It is recommended to implement features in small enough chunks that they can exist
      independently of one another, and only branching off of master.

- Rebase instead of merging.
    + Before you push your changes to the remote server you should rebase against the remote master
      branch.
    + Rebasing onto master ensures the master branch will have a well-organized and linear commit
      history and also gives you an opportunity to immediately fix any conflicts between your branch
      and the master branch before beginning a code review.
    + Merging makes cherry-picking mostly impossible, history navigation cumbersome, and bisection
      extremely difficult - so we always choose rebasing instead.
    + This applies to feature branches as well as the local copy of remote branches.

- Maintain a clean commit history.
    + A commit should have a concise title, a description of the changes contained within, and
      should be a self-contained feature.
    + It's totally fine to have multiple commits in a single branch or PR, as long as they are
      organized accordingly with their titles, descriptions, and contents.
    + Avoid including `merge master into [your branch name]` commits in your PR. This can be done by
      rebasing on the master branch frequently, which can retroactively remove these commits.
    + For help, use [this](conventions/git-tips-and-tricks.md#Cleaning-Up-Your-Commit-History) guide.

- Install Gitleaks to avoid leaking credentials and secure information.
    + Follow [these steps](conventions/git-tips-and-tricks.md#preventing-leaks) to set up and use
      Gitleaks to avoid credential leaks

For any help with using Git or following these these guidelines, please refer to our [Git Tips and
Tricks](conventions/git-tips-and-tricks.md) doc.

## Changelog Guidelines

As changelogs are the aggregation of documented user-facing changes, proper maintenance of
these files is critical for both developers and users. Due to this, we have some guidelines
that attempt to increase consistency and readability of them regarding both format and content.

### Changelog Format

For notable changes, an entry is required in [CHANGELOG.md](CHANGELOG.md) since this file
is used for automated management of bundled release notes. For standardization and validation
purposes, we mandate use of [keep-a-changelog format](https://keepachangelog.com/en/1.0.0/)
for the structure of this file and in many repos we enforce this compliance automatically
through our build process.

The general style of the keep-a-changelog format is similar to this:
```markdown
# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
### Removed
- Entry about another removed item from codebase ([org/repo#123](https://github.com/org/repo/issues/123))

## [0.0.2] - 2020-01-02
### Changed
- Entry about a changed item to codebase ([org/repo#123](https://github.com/org/repo/issues/123))

### Removed
- Entry about a removed item from codebase ([org/repo#123](https://github.com/org/repo/issues/123))

## [0.0.1] - 2020-01-02
### Added
- Added initial functionality foo ([org/repo#123](https://github.com/org/repo/issues/123))

[Unreleased]: https://github.com/org/repo/compare/v0.2.0...HEAD
[0.0.2]: https://github.com/org/repo/compare/v0.0.1...v0.0.2
[0.0.1]: https://github.com/org/repo/releases/tag/v0.0.1
```

### Changelog Content

While the format of the CHANGELOG is important for machine readability of changes, the actual
content of the included changelog entries is even more critical as it is used by end-users.
Because of this, particular care must be dedicated to the choice of inclusion, style, and
wording of these entries.

This list should give you an idea of what _should_ be included in a changelog:

- Any user-facing change (including additions, changes, and removals of features)
- Changes to the public API endpoint contracts
- Performance improvements that are significant enough to be of value to the end-user
- Security fixes
- Changes to supported environments

Some things that **_should not_** be included in the changelog:

- Developer-facing changes (e.g.: test additions, development script changes, etc)
- Refactorings (unless they are significant enough to have risks of new bugs)
- Most documentation changes
- Addition and removal of the same feature within the same release

When writing changelog entries also try to use as concise as you can to describe the change
but don't needlessly avoid mutli-line entries.

**Important**: If a changelog entry is tied to an issue, you **_must_** include a link to that
issue as a trailing fully-expanded link so that cross-referencing can be easily done. The
line below shows an example of an issue-linked changelog entry:
```markdown
- Fix support for using deployment as K8s authentication resource type for Kubernetes >= 1.16
  ([cyberark/conjur#1440](https://github.com/cyberark/conjur/issues/1440))
```

Some more information about general changelog maintenance can also be found [here](https://depfu.com/blog/what-makes-a-good-changelog)
and [here](https://docs.gitlab.com/ee/development/changelog.html).

To put this all together, below are a few examples of good and bad changelog entries:

**Bad entries**:
```markdown
...
# Exclude documentation
- Made links in docs use markdown format

# Irrelevant to end-user
- Added editor tempfiles to `.gitignore`

# Lacking granularity and no issue link
- Fixed issue with dependencies of the project

# Irrelevant to end-user
- Added more tests around API connectivity ([#123](https://github.com/org/repo/issues/123))

# Bad issue links
- Added FIPS compatibility to the agent (#123)
- Added FIPS compatibility to the agent (org/repo#123)
- Added FIPS compatibility to the agent ([#123](org/repo#123))
- Added FIPS compatibility to the agent ([org/repo#123](#123))
...
```

**Good entries**:
```markdown
...
- Added FIPS compatibility to the agent ([org/repo#123](https://github.com/org/repo/issues/123))
- Removed `-n` flag from the accepted CLI flags ([org/repo#234](https://github.com/org/repo/issues/234))
- Improved performance of main API endpoints with change to
  a new router `foo` package dependency
- Fixed CVE-2020-12345 by upgrading `testing` dependency to v3 ([org/repo#345](https://github.com/org/repo/issues/345))
- Fixed overrides handling of `Client` account param [org/repo#456](https://github.com/org/repo/issues/456)
...
```

## Tagging

All projects cyclically get a point where they are ready to package a group of changes as a
check-pointed release which in most cases is started with creating versions through `git tag`.
Git tags create special branches that allow for a reproducible and easy-to-understand
delivery of code that are generally 1:1 mapped with significant feature changes.

In most cases for our projects we use [annotated git tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging#_annotated_tags)
with the name matching the [`v<semver>` tri-dotted pattern](https://semver.org/) (e.g.
`v1.2.3`). By doing this, we make finding relevant code and automating releases easy and
simple. We also use GPG signing of those tags where possible, but this can vary across
projects as our official process for this is still being defined.

To create an annotated tag you have to:
- **Check out the default branch (in most cases this is `master`) and/or the commit that you
  want to tag**. In almost all cases, tags should be created on the default branch for
  automation purposes as a lot of our deliverables get pushed only when the default branch
  has a specific tag. This checkout step is somewhat optional as `git tag` can also take
  in a commit to tag but this procedure is less error-prone vs direct tagging.

  Example of checking out the current upstream main branch history
  ```sh-session
  $ git fetch
  $ git checkout master
  $ git reset --hard origin/master
  ```
- **Verify that the git history looks as expected**. Tools like `git log`, `tig`, `gitk`, and
  others can help you verify that the history is in the expected state.
- **Verify that `NOTICES.txt` looks as expected**. In particular, if the changes in this version
   have modified the project dependencies, this file likely will need an update. In general, this file
   includes info to help us comply with the legal requirements of our open source dependencies,
   including:
  - Legally required copyright notices
  - Legally required license texts
  - Legally required upstream repository links
  - Any other required legal information about the project and its dependencies
- **Verify that the `CHANGELOG.md` content looks as expected**. While most repos already
  have tooling for this included in the CI/CD pipeline, it's always a good idea to verify that:
  - The [changelog guidelines](#changelog-guidelines) were followed, and
  - The tag you are creating has a matching version section in the CHANGELOG (e.g. the `Unreleased`
     changes have been updated to be included in the new version, and there is now an empty
     `Unreleased` section in the CHANGELOG).
- **Create the annotated tag**. To create the tag, use the `git tag -a` command. The main tag
  **must** be in `v<semver>` tri-dotted format:
  ```sh-session
  $ # If you don't have a GPG key set up
  $ git tag -a "v1.2.3" -m "v1.2.3"

  $ # If you do have a GPG key set up
  $ git tag -s "v1.2.3" -m "v1.2.3"
  ```

- **Verify that the tag was created correctly**. You can check this easily with `git describe`:
  ```sh-session
  $ git describe
  v1.2.3
  ```
  If the version returned by `git describe` does not match your created tag, it was not correctly
  created.
- **Push the tag to the upstream repository**. This step makes the tag available to other users
  of the repo:
  ```sh-session
  $ git push origin v1.2.3
  ```

  > Note: Overwriting or removing old tags is extremely discouraged

## GitHub Releases

GitHub releases are the main way that our users consume some of our end products so it is very
important that these are maintained 1:1 along with tags.

> **Note: Only full (i.e. not draft or pre-release) GitHub releases are considered for
> inclusion in the Conjur OSS Suite**

### Draft Release Creation

Once the [tag](#tagging) has been pushed to upstream repository and you are ready to create an
official release of that tagged version we can go to the GitHub UI to first create a draft release:
- **Navigate to the releases page**. In GitHub, under `<main_repo_url>/releases` you can find
  the list of all relases that are available for the repository. We will click the `Draft a new release`
  in the top right to get us into the "new release" page.
- **Fill out the relevant release info**. Make sure that:
  - `Tag version` is the tag you created for this release.
  - `Release title` matches exactly the tag name (`v<semver>`).
  - `Describe this release` is populated with changelog entries for this tagged version. You can
    usually just copy/paste the relevant section from the `CHANGELOG.md` for the version being
    released. If the version header has a link styling (e.g. `[v1.2.3]`) either set the link to
    the tag for this release or remove the brackets from that line.
  - Any files that you may want included this release are attached. This typically includes the
    `LICENSE.md` file, `CHANGELOG.md` file, `NOTICES.txt`, binary executable (if any), SHA256SUM
    of the executable artifacts, etc).
- **Create the draft release**. Check the box `This is a pre-release` and click `Save Draft`
  which will create a draft release that is not yet visible to the public.

Once the draft release is created it's a good time to triple-check the release and ensure that
all of the executable files pass a smoke test for their environments. While this is not strictly
mandatory, it prevents issues with mis-labeled or incompatible binaries.

### Pre-release Publishing

With draft release smoke test completed, we can make a "pre-release" (non-production ready
release) to let the users know that we have a new release but that we are performing a slow
rollout in an effort to ensure low impact if any bugs are found in this new release. This
stage may last as little or as much as needed and it's at the discretion of the maintainers,
but should be guided by things like: the size of user base, cascading impact for bugs, level
of automated testing in the repo, risk of changes causing unintended problems, and other
concerns.

To make a pre-release:
- **Go to the draft release page**. The draft release can be found under
  `<main_repo_url>/releases` for your repo.
- **Publish the pre-release**. Double-check that the `This is a pre-release` is selected and
  click `Publish release`.

### Release Publishing

After some (project-dependent) assurance that the release meets our stability requirements by
the developers and users of the pre-released version of the software, the confidence that the
software works as expected is high. When this stage is reached, we can turn our pre-release
into a full release:
- **Go to the pre-release page**. The pre-release can be found under `<main_repo_url>/releases`
  for your repo.
- **Publish the release**. Double-check that the `This is a pre-release` is **not** selected
  and click `Publish release`.
- **Verify the release publishing**. Ensure that the release is visible in the
  `<main_repo_url>/releases`.

## Open Source Guidelines

For the following instructions, please refer to the `CONTRIBUTING.md` document in the repository you
are working on to determine which steps apply to you.

### When the Repo Includes the CLA

If the `CONTRIBUTING.md` document says you need to sign the CLA, for example:

> "Thanks for your interest in Conjur. Before contributing, please take a moment to read and sign
> our Contributor Agreement. This provides patent protection for all Conjur users and allows
> CyberArk to enforce its license terms. Please email a signed copy to oss@cyberark.com."

Then you **must** submit a signed copy of the CLA to oss@cyberark.com in order for your contribution
to be merged.

A copy of the CLA can be found [here](/documents/CyberArk_Open_Source_Contributor_Agreement.pdf).

### When the Repo Does Not Include the CLA

If the repo does not ask you to sign the CLA, then you may do one of the following:

-  Follow the above instructions for [signing the CLA](#when-the-repo-includes-the-cla).

**OR**

-  Sign your commits using the `--signoff` flag in the `git` CLI (more info
   [here](https://git-scm.com/docs/git-commit#Documentation/git-commit.txt--s)) to certify that you
   have the rights to submit the work under the same license as the project and you agree to a
   Developer Certificate of Origin (see http://developercertificate.org/ for more information).

#### Signing Off a Commit

When signing, every commit must be signed, and your PR will not be approved until this is the case.

To sign-off, use:

    git commit --signoff
or

    git commit -s

Alternatively, if you have already made the commit, you may use:

    git commit --amend --signoff
or

    git commit --amend -s

After amending a commit, you will need to force-push (`push -f`) to your branch for this to take
effect.

> Note: Only repositories licensed under MIT, BSD, or Apache 2.0 are eligible to use the DCO instead
of the CLA for community contributions!!** If the repo does not meet this criteria, you **must**
sign the CLA.

#### Verifying That You Have Signed a Commit

To determine if you **have** signed a commit, look at the commit history in the branch to ensure
each commit includes a line like:

    Signed-off-by: Random J Developer <random@developer.example.org>

This line should include your real name and contact email.
