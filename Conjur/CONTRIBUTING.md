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
* [Appendix](#appendix)
  * [Git-flow Guidelines](#git-flow-guidelines)
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
Please familiarize yourself with our [Code of Conduct](CODE_OF_CONDUCT.md, which details our
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
> our [Git Development Workflow](#Git-flow-Guidelines) first, for following best-practices while
> using source control.

Now that you've chosen a project and an issue and have familiarized yourself with the
project-specific contribution guide, you're ready to start contributing! If you're not sure which
steps to take to get a local copy of the code and start working, you can refer to our general
guidelines for [working on an issue](/CONTRIBUTING.md#working-on-issues) for guidance.

#### Submitting Pull Requests
Once you've completed the work to resolve the issue and ensured your changes are tested
appropriately, it's time to submit your changes for review. Find out more about submitting your PRs
and getting them merged in our [code review guidelines](/CONTRIBUTING.md#code-reviews).

## Appendix

## Git-flow Guidelines
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
    + For help, use [this](conventions/git-tips-and-tricks#Cleaning-Up-Your-Commit-History) guide.

- Install Gitleaks to avoid leaking credentials and secure information.
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
