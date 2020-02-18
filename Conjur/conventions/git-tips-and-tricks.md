
## Git Tips and Tricks

## Table of Contents
- [Cleaning Up Your Commit History](#Cleaning-Up-Your-Commit-History)
- [Interactive Git Rebasing](#interactive-git-rebasing)
- [Rebasing a feature branch off master](#rebasing-a-feature-branch-off-master)
- [Preventing Leaks](#preventing-leaks)

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

## Preventing Leaks

Pushing to github is a form of publication, especially when using a public repo. It is a good idea
to use a hook to check for secrets before pushing code. Normally git hooks are per-clone, which
makes configuring them a burden, however
[core.hooksPath](https://git-scm.com/docs/git-config#Documentation/git-config.txt-corehooksPath)
lets us set a single location git will search for hooks. This way we can configure gitleaks once,
and have git check for secrets before every push.

1. Install gitleaks

       brew install gitleaks
       # OR docker pull zricethezav/gitleaks
       # OR go get -u github.com/zricethezav/gitleaks

   Gitleaks version 3.0 or later is required as the config file format changed in version 2 and 3.0+
   is required for pre-commit verification

2. Configure hooksPath in user git configuration (~/.gitconfig)

       [core]
       hooksPath = ~/git-hooks
3. Create ~/git-hooks/pre-commit and add the following:

       #!/bin/bash -eu

       set -o pipefail

       if ! command -v gitleaks &> /dev/null; then
         echo "ERROR: Gitleaks not installed!"
         exit 1
       fi

       # Provide an escape hatch (for example committing gitleaks config files that contain offending strings)
       if [[ "${SKIP_GITLEAKS:-NO}" == "YES" ]]; then
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
         gitleaks -v --uncommitted --pretty --config=$(git rev-parse --show-toplevel)/.gitleaks.toml
       else
         gitleaks -v --uncommitted --pretty
       fi

4. Make it executable with the following command:

        sudo chmod +x ~/git-hooks/pre-commit
5. If you had a previous gitleaks setup with pre-push, remove that script now: rm
        ~/git-hooks/pre-push

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
+MY_SECRET_KEY=FAKEKEYALKJNDNAI
$ git commit -m "Try to commit a secret"
{
  "line": "MY_SECRET_KEY=FAKEKEYALKJNDNAI",
  "offender": "FAKEKEYALKJNDNAI",
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

Please test your configuration against the conjurinc/playroom repo using a dummy secret such as
`AKIAIOSFODNN7EXAMPLE` which should be recognised as an AWS key.

#### Alternative Hook Configuration: Template Directory
The `core.hooksPath` method works when its safe to apply a single set of hooks to every clone. If
you need to maintain custom hooks for specific repos, then you can use a [template
directory](https://git-scm.com/docs/git-init#_template_directory) instead. This will provide each
clone with a copy of your template hooks, which can then be modified. The disadvantage of this
approach is that if you update the scripts in the template dir, each clone will also need to be
updated.

#### Custom Gitleaks Config
If you need to whitelist certain paths or commits:
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
1. Add any other paths, commits or patterns you need to whitelist

    Note that it is possible to whitelist certain patterns. This option should be chosen over
    whitelisting paths, so that path can still be scanned in future.

       [whitelist]
       regexes = [
         'AKIAIOSFODNN7EXAMPLE'
       ]
1. Commit.