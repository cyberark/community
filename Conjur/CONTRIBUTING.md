# Contributing to the Conjur Open Source Projects

Thanks for your interest in Conjur Open Source! This document serves as a general guide for how to
get started as a contributor. If you have any questions, please ask us on
[Discourse](https://discuss.cyberarkcommons.org)!

## Table of Contents
- [Contributing to the Conjur Open Source
  Projects](#contributing-to-the-conjur-open-source-projects)
  * [Before You Get Started](#before-you-get-started)
    + [Sign the CLA](#sign-the-cla)
    + [Read the Code of Conduct](#read-the-code-of-conduct)
    + [Find Something to Work On](#find-something-to-work-on)
  * [Start Contributing](#start-contributing)
    + [Reporting an Issue](#reporting-an-issue)
    + [Working on Issues](#working-on-issues)
  * [Git-flow Guidelines](#git-flow-guidelines)
  * [Open Source Guidelines](#open-source-guidelines)
    + [When the Repo Includes the CLA](#when-the-repo-includes-the-cla)
    + [When the Repo Does Not Include the CLA](#when-the-repo-does-not-include-the-cla)
      - [Signing Off a Commit](#signing-off-a-commit)
      - [Verifying That You Have Signed a Commit](#verifying-that-you-have-signed-a-commit)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with
markdown-toc</a></i></small>

## Before You Get Started

### Sign the CLA
Before your code can be approved, please read our [CLA](#open-source-guidelines) to ensure you're
compliant with our contributor license agreements.

### Read the Code of Conduct
Please familiarize yourself with our [Code of Conduct](CODE_OF_CONDUCT.md).

### Find Something to Work On

1. Check out [our projects](cyberark.github.io/conjur) to find more information about the tools and
   integrations we're building, and pick one that interests you.

1. Find an issue you'd like to work on using [this
   guide](/CONTRIBUTING.md#finding-issues-to-work-on).

1. Locate the `CONTRIBUTING.md` doc for the project. Typically this file can be found in the
   top-level directory of the project; for example, see the [Secretless Broker
   CONTRIBUTING.md](https://github.com/cyberark/secretless-broker/blob/master/CONTRIBUTING.md). For
   any project, reading this file is the best starting point for contributing, but if no
   `CONTRIBUTING.md` can be found, please feel free to [create an
   issue](/CONTRIBUTING.md#reporting-an-issue) or [submit a PR](/CONTRIBUTING.md#working-on-issues)
   to create one!

   > Note: Some general-purpose guidelines are used across multiple projects, and can be found
   > [here](/CONTRIBUTING.md).

1. Check the project-specific contributing guide for steps for running, building, and testing the
   project. There are usually  prerequisites for installation and setup in these guides that are
   important for getting set up. 

## Start Contributing
Now that you've chosen an project and an issue, and have familiarized yourself with the
project-specific contribution guide, you're ready to start contributing! It's recommended to refer
to the project-specific contribution guide for most things, but here are some general-purpose
workflow steps to refer to.

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
    + Before you push your changes to the remote server you should rebase against the remote master
      branch.
    + Rebasing onto master ensures the master branch will have a well-organized and linear commit
      history and also gives you an opportunity to immediately fix any conflicts between your branch
      and the master branch before beginning a code review
    + Merging makes cherry-picking mostly impossible, history navigation cumbersome, and bisection
      extremely difficult - so we always choose rebasing instead
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
