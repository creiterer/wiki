<!-- TITLE: SVN -->
<!-- SUBTITLE: SVN Cheat Sheet -->

# `svn` Cheat Sheet
## Reverting
* Undo local changes: `svn revert <filename>`
* Revert a file to a certain revision number: `svn up -r <revision-number> <filename>`

## Merging
* Merge changes from certain revision numbers of a certain branch to the current branch (e.g. for backporting from trunk): `svn merge -c<rev-num1>,<rev-num2> <branch> .`. For example: `svn merge -c752277,753640 ^/path/to/trunk .`.

## Show Changes of Certain Revision
* Diff *svn:mergeinfo* property: `svn diff -N .`
* Show changes from a certain revision: `svn diff -c <revision>`
* Show changes between two certain revisions: `svn diff -r <revA>:<revB>`

## Relocating a Repository to a New SVN Server URL
* `svn relocate <new-server-url>`