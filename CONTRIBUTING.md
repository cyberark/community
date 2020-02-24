# Contributing to the Community Repo

Whether you're a member of the CyberArk team, or are just getting involved with our community, you
can help improve our community experience! 

- [Contributing to the Community Repo](#contributing-to-the-community-repo)
  * [Where Do I Start?](#where-do-i-start-)
  * [Contribution Workflow](#contribution-workflow)
    + [Reporting an Issue](#reporting-an-issue)
    + [Working on Issues](#working-on-issues)
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
issue. If it has been created, check out the [working on issues](#working-on-issues) section. If it
hasn't been created, read about [how to report a new issue](#reporting-an-issue!

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
    > kind/documenation kind/enhancement

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

1. Verify that your commit history is clean and organized, and you have rebased on `master` to
   resolve any conflicts. 

1. Submit a `Pull Request` ("`PR`")
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

1. Add the `Implemented` or `In Review` label to the issue, and ask a maintainer to review your
   code.

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