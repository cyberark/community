# Contributing to the Conjur Open Source Projects

Thanks for your interest in Conjur Open Source! This document serves as a general guide for how to
get started as a contributor. If you have any questions, please ask us on [Discourse](https://discuss.cyberarkcommons.org)!

## Table of Contents

- [Contributing to the Conjur Open Source Projects](#contributing-to-the-conjur-open-source-projects)
  * [Where do I start?](#where-do-i-start-)
  * [Contribution Workflow](#contribution-workflow)
    + [Reporting an Issue](#reporting-an-issue)
    + [Working on Issues](#working-on-issues)
  * [Git-flow Guidelines](#git-flow-guidelines)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

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
Refer to our general guidelines for [reporting an issue](/CONTRIBUTING.md#reporting-an-issue)


### Working on Issues
> Note: In addition to understanding the high-level workflow for issues, it is important to review
> our [Git Development Workflow](#Git-flow-Guidelines) first, for following best-practices while
> using source control.

Refer to our general guidelines for [working on issues](/CONTRIBUTING.md#working-on-issues)


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
      organized accordingly with their titles, descriptions, and contents.
    + Avoid including `merge master into [your branch name]` commits in your PR. This can be done by
      rebasing on the master branch frequently, which can retroactively remove these commits.
    + For help, use [this](conventions/git-tips-and-tricks#Cleaning-Up-Your-Commit-History) guide.

- Install Gitleaks to avoid leaking credentials and secure information
    + Follow [these steps](conventions/git-tips-and-tricks.md#preventing-leaks) to set up and use
      Gitleaks to avoid credential leaks

For any help with using Git or following these these guidelines, please refer to our [Git Tips and
Tricks](conventions/git-tips-and-tricks) doc.