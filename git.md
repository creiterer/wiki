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
* Diff of a certain commit: `git diff COMMIT^ COMMIT`, where `COMMIT` is the commit hash of some commit.
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
* Of a particular file: `git log --follow <filename>`

## List Branches
* Show *remote and local* branches: `git branch -a`
* Show *only remote* branches: `git branch -r`
* Show *only local* branches: `git branch`

## Rebase to up-to-date Master Branch
* `git pull --rebase origin master`

## Stashing
* `git stash` to save local modifications to a new stash.
* `git stash pop [stash@{n}]` to apply a stash and remove it from the stash list.
* `git stash apply [stash@{n}]` to apply a stash and keep it in the stash cache.
* `git stash list` to list the stash cache.