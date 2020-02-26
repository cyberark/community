# Contributing to the Community Repo

Whether you're a member of the CyberArk team, or are just getting involved with our community, these
general-purpose guidelines are meant to help you familiarize yourself with our processes. You can
use them when working on any of our public projects, including this one!

## Table of Contents

- [Contributing to the Community Repo](#contributing-to-the-community-repo)
  * [Where Do I Start?](#where-do-i-start-)
  * [Contribution Workflow](#contribution-workflow)
    + [Finding Issues to Work On](#finding-issues-to-work-on)
    + [Reporting an Issue](#reporting-an-issue)
    + [Working on Issues](#working-on-issues)
    + [Submitting a Pull Request](#submitting-a-pull-request)
    + [Getting Your Code Reviewed](#getting-your-code-reviewed)
  * [Tips For Making a Project Open to
    Contributions](#tips-for-making-a-project-open-to-contributions)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with
markdown-toc</a></i></small>

## Where Do I Start?

As you visit the various guides and documents throughout this repository, you may notice something
that you feel is missing, or perhaps you feel it could be improved in some way. This documentation
is used by a wide variety of community members, it's important to us that we are as clear and
thorough as possible, so your perspective is important! Your feedback can help countless others, so
don't be afraid to be the change you want to see! 

## Contribution Workflow
Your first step should be checking the `Issues` tab to see if someone else has already created the
issue. If it has been created, check out the [working on issues](#working-on-issues) section, or
feel free to add additional context or information about the topic. If it hasn't been created, read
about [how to report a new issue](#reporting-an-issue)!

### Finding Issues to Work On 

1. Click the `Issues` tab on Github to see open issues

1. Select an existing issue and provide the following information in a comment:
    - State your intention to work on the issue
    - Provide an outline for your implementation plan  

    This is important to avoid the overlapping of work! 

1. If the issue is already in progress, feel free to ask questions or engage in conversation about
    the implementation. Otherwise, continue on to [working on issues](#working-on-issues).

### Reporting an Issue
1. After confirming that the topic doesn't already exist, you'll need to click `New Issue` to create
   it.

1. Select a template, as this will automatically add an appropriate tag and provide additional
   guidelines for what information is required.

1. Create a descriptive title for the issue, using present-tense verbage, e.g.
    > Secretless Broker does not have emoji support

1. Add the appropriate tag for your issue, if one was not added by the template, e.g.
    > kind/documenation kind/enhancement

1. Continue to monitor the issue for responses and engage in conversation until resolved

### Working on Issues
> Note: In addition to understanding the high-level workflow for issues, it is important to review
> the [Git Development Workflow](#Git-flow-Guidelines) first, for following best-practices while
> using source control.

1. After receiving confirmation that the issue is not already in progress, add the `Implementing`
   label to the issue as you begin to work on it.

1. `Fork` the repository locally. Click
   [here](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) for information
   on how to fork.

1. Create a feature branch to store your changes, using `[Issue Number]-[Name-Of-Issue], e.g.
    > 1004-add-emoji-support

1. Make your changes!

1. Run tests as described in the `CONTRIBUTING.md`, or as outlined in the test stage in the
   `Jenkinsfile`, ensuring they pass

### Submitting a Pull Request
1. Verify that your commit history is clean and organized, and you have rebased on `master` to
   resolve any conflicts. 

1. Navigate to Githhub and open a `Pull Request` ("`PR`") There are two ways you can do this.
   1. On the main page of the repo, or in the `Pull Request` tab, select `New Pull Request`.
   2. If you have recently updated your branch, you should see a notification prompting you to open
      a new pull request from your branch, click the button beside the notification that says `New
      Pull Request`.

1. Make sure you're requesting a merge into `master` from your branch

1. Add a title and a description
    + Add a title to the PR that describes what the set of changes included in the PR accomplishes,
      as well as a reference to the issue it addresses, if an issue exists. The PR title should be
      clear, specific, and succinct.

        * Examples of bad PR titles:

                Component refactor
                Minor fixes
                Add tests

        * Examples of good PR titles:

                #40 - Improved logs for default authenticator
                Bump special-gem version to 1.3.2
                #1645 - Add support for configuring connector plugin via environment

    + Add a description to the PR that details the changes you made, filling out any categories
      listed by a template, and linking the original issue in the description, e.g.
        > Connected to #[Issue Number]

1. Add the `Implemented` or `In Review` label to the issue

1. Tag a reviewer if any are recommended in the righthand menu.

1. Submit the Pull-Request

### Getting Your Code Reviewed
Once your pull-request has been submitted for review, a reviewer will look for a few things.

- A maintainer will verify that any contributor license agreements have been met. Required
  contributor license agreements (if any) are usually documented in the repo's CONTRIBUTING.md.

- A maintainer will review your code, and verify that it addresses the issue sufficiently while
  meeting the contribution guidelines or style patterns for the project.

  Here are a few things a reviewer may look for.
   - Has the branch author done a good job cleaning up the commit history?
   - Has the branch been rebased against master?
   - Has the code been thoroughly tested? 
      - Have you ran any unit or integration tests, and made note of it in the pull-request
        description?
      - Have you performed any manual or non-standard tests, and made note of them in the
        pull-request description?
   - Does this pull-request require an update to any existing documentation? 
      - If so, does an issue need to be made for updating the documentation?
   - Is the code written in a way that is consistent with the existing code base?

- The maintainer will finalize their review 
   - If a reviewer notices an issue with your pull-request, such as those listed above, they will
     request changes be made. You may need to go back and fix a thing or two before it can be
     approved. 
   - If any of the reviewer's feedback is optional, it will be clearly marked "Not required" or
     "nit". It might still be worth addressing, if you can.

- Respond directly to any comments with any of your questions or concerns.

- After making any changes, required or otherwise, make sure your commit history is still organized,
  and make sure you have recently rebased off of master. 

- If changes were requested, you can prompt for a re-review at the bottom of your pull-request's
  page in Github. Otherwise, you can click the 're-review' icon beside the reviewers name on the
  righthand side of your pull-request page.

- From here you will engage in conversation with the reviewer(s) until they are satisfied with the
  branch state, and confirm that it is ready to merge into master. Once the PR is approved (Marked
  as "Approved" in Github), you are ready to merge your changes!

## Tips For Making a Project Open to Contributions
Since standards for contribution can vary from project to project, it's beneficial to use the
following tips to make that information easy to find, and easy to use.

1. The project should be listed in the dropdown-list in [the Community README.md](README.md), under
   its respective team

1. Within the project's own repository, a CONTRIBUTING.md file should be the standard entry-point
   for a contributor, whether internal or external. If it does not exists, it's recommended that one
   is created, and pointed to by the top-level README.md of the project. </br> A good
   CONTRIBUTING.md has the following:
    - A reference to this community repo for general guidelines
    - Where to find issues 
    - How to report new issues
    - How to work on issues
    - Standards for writing in the project-specific language
    - How to build, run, and test the project
    - Any relevant forums for discussion and collaboration
    - Any project-specific best practices

1. Templates for issues can improve the information gathered for a new issue, and provide helpful
   organization, while reducing the amount of domain knowledge required for filing an issue, and
   should be created and wherever possible. For example, templates for common cases like `bugs` or
   `feature requests` can save time and cut down on requests for additional information.