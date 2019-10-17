## reflog
`reflog` shows a log of changes to the local repository `HEAD`

`git reflog <branch>` -- see the commits that you previously squashed

`git log -p <hash>` -- see the changes in the commit

This also helps if you have been rebasing and realized you need to reset, this helps to find the correct commit to reset to

## Stash "added" (and not staged) files, too:
`git stash push -m "NIEGBZH-2707: wip" --include-untracked`

Saves all the files, including untracked

## diff without typing the whole path
How to diff without typing the whole path:

https://stackoverflow.com/questions/14107546/how-to-git-diff-without-typing-the-whole-path

`git diff **/Foo.cs`


## Make git understand rename
Tell git a renamed file is really a rename:

https://stackoverflow.com/questions/4708655/git-renamed-file-manually-git-confused
There is no problem. Simply:

`git rm old`

or even:

`git add -A`

and it will realize that it is a rename. Git will see the delete plus the add with same content as a rename.

## Stash only certain files
Stash only a certain file:

`git stash push -m "message" <path>`

## View stash
View the files in the stash:

`git stash show` - If there is only one stash.

`git stash show stash@{0}` - can specify the stash ID. 

View the diff:

`git stash show -p` - if there is only one stash.

`git stash show -p stash@{0}` - can specify the stash ID.

## --force-with-lease
Do not do 

`git push --force`

DO:

`git push --force-with-lease`

https://developer.atlassian.com/blog/2015/04/force-with-lease/

## log all
`git log --all`

shows the log for all branches

## Submodules
Clone including submodules:

https://stackoverflow.com/questions/3796927/how-to-git-clone-including-submodules

`git clone --recurse-submodules -j8 git://github.com/foo/bar.git`


Update submodules for already cloned repos:

`git submodule update --init --recursive`


If you have updated your submodules and now want to point to the TIP of the submodules project from your main project:

`git submodule update --recursive --remote`

https://stackoverflow.com/questions/1030169/easy-way-to-pull-latest-of-all-git-submodules

## List files in a commit (without the diff)
`git show -r --name-only HEAD`


## Undo changes to a a non-staged file:
`git checkout <file>`

## Merging and rebasing
We are in a feature branch:

`git rebase develop` -- rebases current onto `develop`. The current branch will be aware of all the changes in `develop`.

`git merge develop` -- merges `develop` into the current branch. The current branch will be aware of all the changes in `develop`.

## gitk

`gitk <file path>` -- see history for one file

## Git revert commit

`git revert <commit> -m 1`

https://stackoverflow.com/questions/5970889/why-does-git-revert-complain-about-a-missing-m-option
