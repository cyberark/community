
## Git Tips and Tricks

## Table of Contents
- [Git Tips and Tricks](#git-tips-and-tricks)
- [Cleaning Up Your Commit History](#cleaning-up-your-commit-history)
- [Interactive Git rebasing](#interactive-git-rebasing)
- [Rebasing a feature branch off master](#rebasing-a-feature-branch-off-master)
- [Preventing Leaks](#preventing-leaks)
    + [Alternative Hook Configuration: Template Directory](#alternative-hook-configuration--template-directory)
    + [Custom Gitleaks Config](#custom-gitleaks-config)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


## Cleaning Up Your Commit History

A branch author can use the instructions below to maintain a clean commit history and submit PRs
that are well-organized and easier to review. When following this workflow, the commits in the
branch PR should always only encapsulate logical groupings of code changes, nothing more and nothing
less.

It's worth noting that at times squashing and reordering your history is nontrivial, but putting in
the effort to have a clean commit history pays off long-term in the maintenance and onboarding costs
for your repository. If you start working through these instructions and find that the history of
the feature branch is too tangled, you should ask for help.

[This
page](https://github.com/mockito/mockito/wiki/Using-git-to-prepare-your-PR-to-have-a-clean-history)
has pretty good info on the basics of doing this in practice, but for convenience we also include a
simple explanation below.

Let's start with a messy local branch (before opening a PR and getting back PR comments) that looks
something like this:
```text
|\
| - added feature #1
| - feature #2
| - unrelated change "A"
| - more work on feature #1
|/
<other history>
```

The first good step the author should take is to squash the `more work on feature #1` onto the
commit `added feature #1` using an [interactive Git rebase](#interactive-git-rebasing) and reword
the `feature 2` commit:

```text
|\
| - added feature #1
| - added feature #2
| - unrelated change "A"
|/
<other history>
```

Let's assume that the branch was submitted for a PR review in the revised state above (so that the
branch has now been pushed to the remote GitHub server). After responding to code review comments,
the author adds more commits on their local branch (keeping feature-related changes in separate
commits) so that the branch commit history now looks similar to this:

```text
|\
| - added feature #1
| - added feature #2
| - unrelated change "A"
| - PR comment fix of feature #1
| - PR comment fix of feature #2
| - More PR comment fixes for feature #2
|/
<other history>
```

To clean this up, the author would squash (using the interactive rebase again):

- `PR comment fix of feature #1` into `added feature #1`
- `PR comment fix of feature #2` and `More PR comment fixes for feature #2` into `feature #2`

The end result after rebasing would be the history below, which looks similar to the branch commit
history when the PR was opened but it now includes all of the code review fixes:

```text
|\
| - added feature #1
| - added feature #2
| - unrelated change "A"
|/
<other history>
```

Once the author is done with rebasing, they then force-push (`git push origin -f HEAD`) their branch
up to origin to overwrite the old branch with this new history.

With a clean git history as above, PR reviewers can use the standard `merge` button to merge the PR
so the code will be available on the default branch (eg `master`).

## Interactive Git rebasing

Given the following history:
```
|\
| - added feature #1
| - feature #2
| - unrelated change "A"
| - more work on feature #1
|/
<other history>
```

To do you would use an interactive git rebase like this:
```
$ git rebase -i HEAD~4
```

_Note that the second column in the example here will be the hash of the commit and we're just using
a placeholder_

And changing the view from this:
```
pick abab1234 added feature #1
pick cdcd5678 feature #2
pick efef90ab unrelated change "A"
pick ghghcdef more work on feature #1
```

To:
```
pick abab1234 added feature #1
f cdcd5678 more work on feature #1
r efef90ab feature #2
pick ghghcdef unrelated change "A"
```

After saving and exiting, you will have squashed the feature #1 commits into a single logical unit
and opened the editor to fixup `feature #2` title into `added feature #2`. The new history should
look like this:

```
|\
| - added feature #1
| - added feature #2
| - unrelated change "A"
|/
<other history>
```

## Rebasing a feature branch off master

### From a branch in the main project

If you are in a feature branch of a repository cloned on your local machine
```
git checkout feature-branch
```
you can rebase your feature branch onto master by running
```
git rebase origin/master
```

If you have already pushed your branch to the remote server, you'll need to force push to sync the
remote with your local changes:
```
git push --force
```

For more info on rebasing, especially on rebasing vs merging, see
[here](https://git-scm.com/book/en/v2/Git-Branching-Rebasing).

### From a fork

If you are working from a fork, then from the command line in the root directory of the project on
your local machine, set the upstream:
```
git remote add upstream https://github.com/org/repo
```

Fetch all the branches of the remote upstream project:
```
git fetch upstream
```

Rewrite your local branch to replay any commits from your local branch on top of the `upstream/master`:
```
git rebase upstream/master
```

Review the git logs before publishing these changes to ensure the git history looks as expected:
```
git log
```

Force push your changes to your remote fork:
```
git push -f origin master
```

## Preventing Leaks

Pushing to github is a form of publication, especially when using a public repo. It is a good idea
to use a hook to check for secrets before pushing code. Normally git hooks are per-clone, which
makes configuring them a burden, however
[core.hooksPath](https://git-scm.com/docs/git-config#Documentation/git-config.txt-corehooksPath)
lets us set a single location git will search for hooks. This way we can configure gitleaks once,
and have git check for secrets before every push.

1. Install gitleaks

    ```sh
    brew install gitleaks
    ```
    Gitleaks version 7.1.0 or later is required

1. Configure hooksPath in user git configuration
    ```sh
    vi  ~/.gitconfig
    ```
    ```ini
    [core]
        hooksPath = ~/git-hooks
    ```

1. Create pre-commit hook:

    ```sh
    mkdir ~/git-hooks/
    vi ~/git-hooks/pre-commit
    ```
    Add the following:
    ```sh
    #!/bin/bash -eu

    set -o pipefail

    if ! command -v gitleaks &> /dev/null; then
      echo "ERROR: Gitleaks not installed!"
      exit 1
    fi

    # Provide an escape hatch (for example committing gitleaks config files that contain offending strings)
    if [[ "${SKIP_GITLEAKS:-NO}" != "NO" ]]; then
      echo SKIPPING GIT LEAKS AS ENV VAR IS SET
      exit 0
    fi

    # Provide a helpful error message for repos with no commits
    if ! git rev-parse HEAD &> /dev/null; then
      echo "It looks like this repo has just been initialised and has no commits.
    Gitleaks requires at least one commit to exist in the repo.
    Please create an empty root commit:
        git reset; SKIP_GITLEAKS=YES git commit --allow-empty -m initial
    then add and commit your code."
      exit 1
    fi

    if git ls-files $(git rev-parse --show-toplevel)| grep -q '.gitleaks.toml' &> /dev/null; then
      gitleaks -v --leaks-exit-code=1 --config-path=$(git rev-parse --show-toplevel)/.gitleaks.toml
    else
      gitleaks -v --leaks-exit-code=1
    fi
    ```

1. Make it executable with the following command:

    ```sh
    chmod +x ~/git-hooks/pre-commit
    ```
    NOTE: If you had a previous gitleaks setup with pre-push, remove that script now:

    ```sh
    rm ~/git-hooks/pre-push
    ```
1. Test
    ```sh
    mkdir ~/gitleaks-test
    cd ~/gitleaks-test
    git init
    SKIP_GITLEAKS=YES git commit --allow-empty -m initial
    echo 'AKIAIOSFODNN7EXAMPLE' > test.txt
    git add test.txt
    git commit -m "gitleaks test"
    #THIS SHOULD FAIL WITH A GITLEAKS ERROR, please proceed if so
    #if it does not, please double check the previous steps
    cd ~
    rm -rf ~/gitleaks-test
    ```
    And you're done! :)

<details><summary>Example commit that contains an AWS key</summary>
Note: AWS key is one that is in the exceptions list for the docs repository

```
$ git diff --cached
diff --git a/contains_aws_key b/contains_aws_key
new file mode 100644
index 0000000..cc3e837
--- /dev/null
+++ b/contains_aws_key
@@ -0,0 +1 @@
+MY_SECRET_KEY=AKIAIOSFODNN7EXAMPLE
$ git commit -m "Try to commit a secret"
{
  "line": "MY_SECRET_KEY=AKIAIOSFODNN7EXAMPLE",
  "offender": "AKIAIOSFODNN7EXAMPLE",
  "commit": "7d5beda3daae114ce1f42e2cdf30c212cef00zzz0",
  "repo": "testproject",
  "rule": "AWS Client ID",
  "commitMessage": "Adding it in\n",
  "author": "Larry Leak",
  "email": "larry.leak@secretful.com",
  "file": "contains_aws_key",
  "date": "2019-11-25T15:56:49-06:00",
  "tags": "key, AWS"
}
WARN[2019-11-25T16:02:28-06:00] 1 leaks detected in staged changes
```
</details>
<br>

## Alternative Configurations

#### Template Directory
The `core.hooksPath` method works when its safe to apply a single set of hooks to every clone. If
you need to maintain custom hooks for specific repos, then you can use a [template
directory](https://git-scm.com/docs/git-init#_template_directory) instead. This will provide each
clone with a copy of your template hooks, which can then be modified. The disadvantage of this
approach is that if you update the scripts in the template dir, each clone will also need to be
updated.

#### Custom Gitleaks Config
If you need to exclude certain paths or commits:
1.  copy [gitleaks.toml](https://github.com/zricethezav/gitleaks/blob/master/gitleaks.toml) and add
    it to your repository. Note that the curl method will retrieve an up to date rule set, using
    `gitleaks --sample-config` may lead to out of date patterns being used.

        curl https://raw.githubusercontent.com/zricethezav/gitleaks/master/gitleaks.toml > .gitleaks.toml
1. Add `.gitleaks.toml` to the whitelist section:

       [whitelist]
       files = [
         "(.*?)(jpg|gif|doc|pdf|bin)$",
         ".gitleaks.toml"
       ]
1. Add any other paths, commits or patterns you need to exclude

    Note that it is possible to exclude patterns. This option should be chosen over
    excluding paths, so that if other secrets are leaked into the same file(s) in future, they will be caught.

       [whitelist]
       regexes = [
         'AKIAIOSFODNN7EXAMPLE'
       ]
1. Commit.
