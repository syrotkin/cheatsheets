# diff, log, show

## reflog
`reflog` shows a log of changes to the local repository `HEAD`

`git reflog <branch>` -- see the commits that you previously squashed

`git log -p <hash>` -- see the changes in the commit

This also helps if you have been rebasing and realized you need to reset, this helps to find the correct commit to reset to

## diff without typing the whole path
How to diff without typing the whole path:

https://stackoverflow.com/questions/14107546/how-to-git-diff-without-typing-the-whole-path

`git diff **/Foo.cs`

## log all
`git log --all`

shows the log for all branches

## List files in a commit (without the diff)
`git show -r --name-only HEAD`

## Show the log of a different branch
`git log <branch_name>`

# Make git understand rename
Tell git a renamed file is really a rename:

https://stackoverflow.com/questions/4708655/git-renamed-file-manually-git-confused
There is no problem. Simply:

`git rm old`

or even:

`git add -A`

and it will realize that it is a rename. Git will see the delete plus the add with same content as a rename.

# --force-with-lease
Do not do 

`git push --force`

DO:

`git push --force-with-lease`

https://developer.atlassian.com/blog/2015/04/force-with-lease/


# Branches

## Rename current branch

`git branch -m <new_name>`

## Merging and rebasing
We are in a feature branch:

`git rebase master` -- rebases current onto `master`. The current branch will be aware of all the changes in `master`.

`git merge master` -- merges `master` into the current branch. The current branch will be aware of all the changes in `master`.

## Delete local branches that do not exist in remote anymore
```
git fetch -p
git branch -vv | grep ': gone]' | awk '{print $1}' | xargs git branch -D
```

https://stackoverflow.com/questions/7726949/remove-tracking-branches-no-longer-on-remote

Adding it as an alias (note the `!git` prefix):
```
[alias]
	deletegonebranches = !git branch -vv | grep ': gone]' | awk '{print $1}' | xargs git branch -D
```

## Cherry pick
```
git cherry-pick <commit_sha>
```
This will cherry pick commit <commit_sha> from the respective branch **into the current branch**

## Interactive rebase
```
git rebase -i <last_commit_you_definitely_keep>
```
`<last_commit_you_definitely_keep>` will not be included in the list of commits to pick or drop.


# Undo
## Undo changes to a a non-staged file:
`git checkout <file>`

## Git revert commit

`git revert <commit> -m 1`

https://stackoverflow.com/questions/5970889/why-does-git-revert-complain-about-a-missing-m-option

## Revert changes to a specific file
`git checkout HEAD~1 -- /file/to/restore`

or

`git checkout <commit_hash> -- /file/to/restore`

https://stackoverflow.com/questions/215718/how-can-i-reset-or-revert-a-file-to-a-specific-revision


# Remotes

## List remotes:
```
git remote -v
```

## Update remote:
```
git remote set-url origin <url>
```

## set-upstream
`git push --set-upstream origin <branch-name>`


# gitk

`gitk <file path>` -- see history for one file


# Stash

## Stash "added" (and not staged) files, too:
`git stash push -m "NIEGBZH-2707: wip" --include-untracked`

Saves all the files, including untracked

## Stash only certain files
Stash only a certain file:

`git stash push -m "message" <path>`

## List stashes
`git stash list`

## View files in stash
View the files in the stash:

`git stash show` - If there is only one stash.

`git stash show stash@{0}` - can specify the stash ID. 

View the diff:

`git stash show -p` - if there is only one stash.

`git stash show -p stash@{0}` - can specify the stash ID.


# Config

## List all

`git config -l`

`git config --local -l`

`git config --global -l`

`git config --system -l`

## Configure the name and email address:
### Globally:
```
git config --global user.name "Your Name"
git config --global user.email "youremail@yourdomain.com"
```
### For one repository:
```
git config user.name "Your Name"
git config user.email "youremail@yourdomain.com"
```

## Configure default editor:
Configures VS Code as the default editor:
```
git config --global core.editor "code --wait"
```

## Change the author of the previous commit 
From: https://www.git-tower.com/learn/git/faq/change-author-name-email/

```
git commit --amend --author="John Doe <john@doe.org>"
```

## Example of file under C:\Program Files\git\etc\gitconfig
```
[diff "astextplain"]
	textconv = astextplain
[filter "lfs"]
	clean = git-lfs clean -- %f
	smudge = git-lfs smudge -- %f
	process = git-lfs filter-process
	required = true
[http]
	sslBackend = openssl
	sslCAInfo = C:/Program Files/Git/mingw64/etc/ssl/certs/ca-bundle.crt
[core]
	autocrlf = true
	fscache = true
	symlinks = false
[pull]
	rebase = false
[credential]
	helper = manager
[credential "https://dev.azure.com"]
	useHttpPath = true
[init]
	defaultBranch = master
[alias]
	deletegonebranches = !git branch -vv | grep ': gone]' | awk '{print $1}' | xargs git branch -D
```

## Example of C:\Users\Oleksiy.Syrotkin.DEV-ZH-321\.gitconfig
```
[safe]
	directory = C:/dev
	directory = C:/dev/practice/github/cheatsheets
[core]
	editor = code --wait
```

# Submodules
Clone including submodules:

https://stackoverflow.com/questions/3796927/how-to-git-clone-including-submodules

`git clone --recurse-submodules -j8 git://github.com/foo/bar.git`


Update submodules for already cloned repos:

`git submodule update --init --recursive`


If you have updated your submodules and now want to point to the TIP of the submodules project from your main project:

`git submodule update --recursive --remote`

https://stackoverflow.com/questions/1030169/easy-way-to-pull-latest-of-all-git-submodules
