# Contributing to the Conjur Open Source Projects

Thanks for your interest in Conjur Open Source! This document serves as a general guide for how to
get started as a contributor. If you have any questions, please ask us on [Discourse](https://discuss.cyberarkcommons.org)!

## Table of Contents

- [Where Do I Start](#where-do-i-start)
- [Contribution WorkFlow](#contribution-workflow)
    + [Creating an Issue](#creating-an-issue)
    + [Working on Issues](#working-on-issues)
- [Git-Flow Guidelines](#git-flow-guidelines)
- [Testing](#Testing)
    + [Testing Patterns](#testing-patterns)
    + [Running Tests](#running-tests)


## Where do I start?
Each Conjur repository has its own `CONTRIBUTING.md` which details how you can get involved with
contributing to one of our projects. Typically this file can be found in the top-level directory of
the project; for example, see the [Secretless Broker
CONTRIBUTING.md](https://github.com/cyberark/secretless-broker/blob/master/CONTRIBUTING.md). For any
project, reading this file is the best starting point for contributing, but if no `CONTRIBUTING.md`
can be found, please feel free to create an issue or submit a PR to create one!

Additionally, be sure to check out our [Open Source Guidelines](documents/open-source-guidelines.md)
for information on our open source license terms. 

## Contribution Workflow
While it is recommended to refer to the project-specific CONTRIBUTING.md doc first, the following
are general-purpose workflows to reference when working on one of our projects.

### Reporting an Issue
1. Click the `Issues` tab on Github to see open issues, and make sure there isn't already a ticket
   created for your topic.
    - If the topic *does* exists, feel free to contribute to the conversation! Additional
      information about a bug or suggestions for implementation of a feature is always welcome.
    - If the topic *does not* exist, continue through the following steps to create a new issue. 

1. After confirming that the topic doesn't exist, you'll need to click `New Issue` to create it.

1. Select a template, as this will automatically add an appropriate tag and provide additional
   guidelines for what information is required.

1. Create a descriptive title for the issue, using present-tense verbage, e.g.
    > Secretless Broker does not have emoji support

1. Add the appropriate tag for your issue, if one was not added by the template, e.g.
    > kind/bug kind/enhancement

1. Continue to monitor the issue for responses and engage in conversation until resolved

### Working on Issues
> Note: In addition to understanding the high-level workflow for issues, it is important to review
> the [Git Development Workflow](#Git-flow-Guidelines) first, for following best-practices while
> using source control.

1. Click the `Issues` tab on Github to see open issues 

1. Select an existing issue and provide the following information in a comment:
    - State your intention to work on the issue
    - Provide an outline for your implementation plan  

    This is important to avoid the overlapping of work! 

    If the issue is already in progress, feel free to ask questions or engage in conversation about
    the implementation.

1. After confirming that the issue is not already in progress, add the `Implementing` label to the
   issue as you begin to work on it.

1. `Fork` the repository locally. Click
   [here](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) for information
   on how to fork.

1. Create a feature branch to store your changes, using `[Issue Number]-[Name-Of-Issue], e.g.
    > 1004-add-emoji-support

1. Make your changes!

1. Run tests as described in the `CONTRIBUTING.md`, or as outlined in the test stage in the
   `Jenkinsfile`, ensuring they pass

1. Verify that your commit history is clean and organized, and you have rebased on `master` to resolve any conflicts. 

1. Submit a `Pull Request` ("`PR`")
    + Add a title to the PR that describes what the set of changes included in the PR accomplishes. The PR title should be clear, specific, and succinct.

        * Examples of bad PR titles:

                Component refactor
                Minor fixes
                Add tests

        * Examples of good PR titles:

                Improved logs for default authenticator
                Bump special-gem version to 1.3.2
                Add support for configuring connector plugin via environment

    + Add a description to the PR that details the changes you made, filling out any categories listed by a template, and linking the original issue in the description, e.g.
        > Connected to #[Issue Number]

1. Add the `Implemented` or `In Review` label to the issue, and ask a maintainer to review your
   code.


## Git-flow Guidelines
The following guidelines are used to maintain a clean and consistent source control history, and are
important to follow when developing.

- Avoid branching off of branches
    + Branching off of branches can muddle your git history, or make things harder to track and
      maintain when the parent branch changes.
    + It is recommended to implement features in small enough chunks that they can exist
      independently of one another, and only branching off of master.

- Rebase over merging
    + Before you push your changes to the remote server you should rebase against the remote master branch.
    + Rebasing onto master ensures the master branch will have a well-organized and linear commit history and also gives you an opportunity to immediately fix any conflicts between your branch and the master branch before beginning a code review
    + Merging makes cherry-picking mostly impossible, history navigation cumbersome, and bisection extremely difficult - so we always choose rebasing instead
    + This applies to feature branches as well as the local copy of remote branches

- Maintain a clean commit history
    + A commit should have a concise title, a description of the changes contained within, and
      should be a self-contained feature.
    + It's totally fine to have multiple commits in a single branch or PR, as long as they are
      organized accordinly with their titles, descriptions, and contents.
    + Avoid including `merge master into [your branch name]` commits in your PR. This can be done by
      rebasing on the master branch frequently, which can retroactively remove these commits.
    + For help, use [this](conventions/git-tips-and-tricks#Cleaning-Up-Your-Commit-History) guide.

- Install Gitleaks to avoid leaking credentials and secure information
    + Follow [these steps](conventions/git-tips-and-tricks.md#preventing-leaks) to set up and use
      Gitleaks to avoid credential leaks

For any help with using Git or following these these guidelines, please refer to our [Git Tips and
Tricks](conventions/git-tips-and-tricks) doc.