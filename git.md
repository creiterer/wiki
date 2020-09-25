<!-- TITLE: Git -->
<!-- SUBTITLE: Git Cheat Sheet -->

# `git` Cheat Sheet
## Undo Last Commit
### Short Summary
* `git reset HEAD~`
* `git reset HEAD^`

### Detailed Explanation
Source: https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-commits-in-git

```text
$ git commit -m "Something terribly misguided"             # (1)
$ git reset HEAD~                                          # (2)
<< edit files as necessary >>                              # (3)
$ git add ...                                              # (4)
$ git commit -c ORIG_HEAD                                  # (5)
```

1. This is what you want to undo.
2. This leaves your working tree (i.e. the state of your files on disk) unchanged but undoes the commit and leaves the changes you committed unstaged. If you *only* want to *add* more changes to the previous commit, or change the commit message [1], you could use `git reset --soft HEAD~` instead, which is like `git reset HEAD~` (where `HEAD~` is the same as `HEAD~1`) but leaves your existing changes staged.
3. Make corrections to working tree files.
4. `git add` anything that you want to include in your new commit.
5. Commit the changes, reusing the old commit message. `git reset` copied the old head to `.git/ORIG_HEAD`. Therefore, `git commit` with `-c ORIG_HEAD` will open an editor, which initially contains the old commit message and allows to edit it. If you do not need to edit the message, you could use the `-C` option.

[1] Note, that you do not need to reset to an earlier commit if you just made a mistake in your *commit message*. The easier option is to `git reset` (to upstage any changes you have made since) and then `git commit --amend`, which will open your default commit message editor pre-populated with the last commit message.

## Determine Repository URL
* If referential integrity has been broken: `git config --get remote.origin.url`
* If referential integrity is intact: `git remote show origin`

## Showing Diffs
* Diff of an individual file: `git diff <filename>`
* Diff of all changed files: `git diff`
* Diff of a certain commit: `git diff <commit-hash>^ <commit-hash>`
* Diff of staged files: `git diff --staged <filename>`

## Revert Changes of Working Copy
* Single file: `git checkout <filename>`
* Whole directory: `git checkout .`

## Revert Changes Made to the Index
*Warning: This will reset all of your unpushed commits to master*
`git reset`

## Remove Untracked Files/Directories
* Files: `git clean -f`
* Directories: `git clean -fd`

## Blame/Annotate a File
This shows what revision and which author has last modified each line of a certain file.
* `git blame <filename>`
* `git annotate <filename>`

## Show Log Messages
* `git log`
* Show only the name of the changed files: `git log --name-only`
* Of a particular file: `git log --follow <filename>`

## Show Files of a Certain Commit
* `git show --name-only <commit-hash>`

## List Branches
* Show *remote and local* branches: `git branch -a`
* Show *only remote* branches: `git branch -r`
* Show *only local* branches: `git branch`

## Rebase to up-to-date Master Branch
* `git pull -r|--rebase origin master`

## Stashing
* `git stash` to save local modifications to a new stash.
* `git stash pop [stash@{n}]` to apply a stash and remove it from the stash list.
* `git stash apply [stash@{n}]` to apply a stash and keep it in the stash cache.
* `git stash list` to list the stash cache.
* `git stash show [stash@{n}]` to show the files that changed in the (most recent if no concrete stash is specified) stash.
* `git stash show -p [stash@{n}]` to show the diff of a stash.
* `git stash push [-m message] <path>` to stash a specific path.

## Recover Deleted Files
Source: https://stackoverflow.com/questions/11956710/git-recover-deleted-file-where-no-commit-was-made-after-the-delete
1. `git reset HEAD <file>`
2. `git checkout <file>`

## Switch to Another Tag
Source: https://stackoverflow.com/questions/4330610/switch-to-another-git-tag
* `git checkout tags/<tag>`
* shorthand (only safe if the repository does not have a branch with the same name): `git checkout <tag>`

## Checkout Specific Revision
Source: https://stackoverflow.com/questions/215718/reset-or-revert-a-specific-file-to-a-specific-revision-using-git
* revert to a certain commit (specified by `commit-hash`): `git checkout <commit-hash>`
* revert certain files to a certain commit (specified by `commit-hash`): `git checkout <commit-hash> -- <file1> <file2> ... <filen>`
* revert to the commit before a certain commit (specified by `commit-hash`): `git checkout <commit-hash>~1 -- <file1> <file2> ... <filen>`

## Revert Certain Commits
* `git revert <commit-hash-1> <commit-hash-2> ... <commit-hash-n>`

## Push Certain Commits
For example, pushing all but the last 5 commits to `origin` on branch `branch`: `git push origin HEAD~5:<branch>`

## Cherry-Pick a Commit
Source: https://www.devroom.io/2010/06/10/cherry-picking-specific-commits-from-another-branch
* `git cherry-pick <commit-hash>`, where `commit-hash` is the commit hash of the desired commit on another branch.

## Squashing of Commits
See https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History
1. `git rebase -i [--autosquash] <commit-hash>`, where `commit-hash` is the parent of the last commit you want to edit. For example,
`git rebase -i HEAD~3` will edit the last three commits. To automatically squash `fixup` or `squash` commits, use the [--autosquash](https://git-scm.com/docs/git-rebase#Documentation/git-rebase.txt---autosquash) option.
2. replace `pick` with `squash` to squash some commit into the previous one.

## Renaming Branches
Source: https://linuxize.com/post/how-to-rename-local-and-remote-git-branch/
1. `git checkout <old_name>`, to switch to the local branch `old_name` that should be renamed.
2. `git branch -m <new_name>`, to rename the local branch to `new_name`.
At this point, the local branch is renamed. If `old_name` is already pushed to the remote repository, the next two steps are necessary to also rename the remote branch.
3. `git push origin -u <new_name>`, to push `new_name`.
4. `git push origin --delete <old_name>`, to delete the `old_name` remote branch.