Configurations
======
To start a new git:
```
git init
```

##### Location of config file and ignore file
```
~/.gitconfig
~/.gitignore
```

##### Command to get help
```
git help <command>
```

##### Command to check config
```
git config --list
```

##### Command to check file status
```
git status
```

##### Status with details
```
git status -p
```

Key commands
======

##### update github from local (to share in github)
```
git push origin master
```

##### update local from github (get shared from github)
```
git fetch origin
```

Log
======

######  one line log info
```
git log --pretty=oneline
git log --oneline --decorate
```

######  Command to log info with full graph
```
git log --oneline --decorate --graph --all
```

######  Command to check log file
```
git log --stat
git log --graph
```

###### Command to show remote log
```
git log remotes/origin/master --graph --oneline
```

###### Command to list all files
```
git ls-files
git ls-files --stage
```

Basics
======

##### Command to add files to staging
```
git add <filenames>
```

###### Command to delete staged files
```
git rm <filenames>
```

###### Command to take staged files back
```
git reset <filenames>
```

###### Command to move files
this is equivalent to rename file, delete from git repository and add to repository
```
git mv <file_from> <file_destination>
```

###### Commnad to commit all changes
```
git commit -m "comment"
```

##### Command to commit without staging (all modified files are committed)
```
git commit -a -m "comment"
```

##### Command To remove the whole repository
```
rm -rf .git
```

##### Command to specify ignore files
```
git config --global core.excludesfile ~/.gitignore
```

Undo
======

###### Command to amend commit: the second commit replaces the first
```
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

###### Command to unstage a staging file
```
git reset HEAD <file>
```

###### Command to undo a modified file
```
git checkout -- <file>
```

Remote
======

###### Command to show all URLs that Git stored
```
git remote -v
```

###### Command to add additional remote url
```
git remote add <name> <url>
e.g. git remote add pb  https://github.com/paulboone/ticgit
```

###### Command to change remote URL
```
git remote set-url origin <url>
```

###### Command to inspect a remote
```
git remote show origin
```

###### Command to rename remote alias
```
git remote rename <old_alias> <new_alias>
e.g. git remote rename pb paul
```

###### Command to remove remote site
```
git remote rm <remote_name>
e.g. git remote rm pb
```

Github
======
###### Command to register github remote site
```
git remote add origin <repository url> (e.g. https://github.com/francis-fra/R_code.git)
```

###### Command to push with a branch name
```
git push -u origin master
```

###### Command to fetch and merge with the repository in github
```
git pull origin master
```

###### Command to save credentials in cache
```
git config --global credential.helper 'cache --timeout=3600'
```

##### Command to replace unmodify files
NOTE: this will replace modified files completely without any backup!!
```
git checkout -- <file_name>
```

Repository
======

###### Comand to show commit summary
e.g. show current: git show HEAD --oneline --stat
```
git show <id> --oneline --stat
```


Fetch
======
It downloads only but does not merge!! - to get the changes from the remote (synchronize) and fetching from remote (e.g. origin)

```
git fetch <remote_name>
```

To get a remote repository not yet in local, it will also move the origin/master pointer at local
```
e.g.
git fetch origin
```

Pull: fetch + merge
======
pull command automatically fetch and then merge (fetch + merge)
```
git pull
```

alternatively,
```
git pull origin master
```

Push - share
======
publish to the remote works only when no one else has pushed before you.
Ff the remote has changed by someone, then need to fetch first before push again
```
git push <remote_name> <local_branch_name>
# e.g.
git push origin master
```

Tag
======
###### Command to add
```
git tag -a <tag_name> -m "comment"
```

###### show
```
git tag
```

###### to examine check point using tag
```
git show <tag_name>
```


Diff
======

###### compare current (not staged) with last commit
```
git diff
```

###### compare staged changes to last commit
```
git diff --staged
```

###### linux command
```
diff -u old_file new_file
git diff old_file new_file
```

###### check differences of file since last commit
```
git diff -- current_file
```

###### difference between github and local
```
git diff master origin/master
```

###### to restore the previous version
```
git checkout old_version_id
```

###### to compare two branched
```
git diff <branch_01> <branch_02>
```

Branches
======

The default branch name is master, and after making commit, the master branch moves forward automatically to the current branch. The current branch is identified by a pointer called HEAD:

```
git branch
```

###### Command to create a new branch (like creating a pointer)
```
git branch <branch_name>
```

###### Command to switch branch
In other words,  move the HEAD pointer
```
git checkout <branch_name>
e.g. git checkout testing
```

###### Command to create a branch and switch to it
```
git checkout -b <branch_name>
```

###### Command to delete a branch
```
git branch -d <branch_name>
```


Basic branch management
======

###### Command to show all branches and commits
```
git show-branch
```

###### Command to list all branches (including remote)
```
git branch -a
```

###### Command to list all remote branches
```
git branch -r
```

###### Command to list the last commit of each branch
```
git branch -v
git branch -vv
```

###### Command to list branch that merged (or no-merged) with current
```
git branch --merged
git branch --no-merged
```

###### Command to switch to previous tag
```
git checkout tags/<tag_name>
```

###### Command to move (recreate) master back to origin (remote) or other branch
```
git checkout -B master origin/master
```

###### Command to checkout old commit and create a new branch
```
git checkout -b <branch_name> <id>
e.g. git checkout -b oldbranch 49d43de
```

Merge
======
###### Fast forward merge
Suppose that a new branch is directly ahead of the master, in order to join the master with the new branch, so they are pointed to the same snapshot:
```
git checkout master
git merge <branch_name>
```

###### Command to fork - recursive merge
Merge two branches with a common ancestor - the result is that a new snapshot is created by joining the two branches
```
git checkout master
git merge <branch_name>
```

###### Command to merge with graphical display
```
git mergetool
```

###### Command to merge the remote git with the local git
This will create a new branch in the local, called origin/master to synchronize
```
git fetch origin
```

###### Command to save saved authentication in git
```
git config --global credential.helper cache.
```


###### Command to rename a branch
```
git branch -m <old_name> <new_name>
```

###### Command to show commit id
```
git show <commit_id>
```

Tracking branches
======
###### Checking out a local branch from remote branch
```
git checkout -b <branch> <remote>/<branch>
```

e.g. To create a new branch sf based on remote branch serverfix:
```
git checkout -b sf origin/serverfix
```
equivalently,
```
git checkout --track <remote>/<branch>
```

###### Command to retrieve old commit and create a new branch
```
git checkout -b <new_name> <old_commit>
```

Rebasing
======
###### Command to make a cleaner history

e.g. to merge two branches
```
git checkout bh
git rebase master
```

Now bh is ahead of master with all the differences are merged, then do a fast forward merge
```
git checkout master
git merge bh
```

Remote branch
======
###### Command to show remote details
```
git ls-remote [remote]
git remote show [remote]
```

###### Command to delete remote branches
```
git push <remote_name> --delete <branch_name>
```

###### Command to rebase
Instead of merging the two branches and create a new one, the rebase command merge the changes and pointed to it while the master branch stays where it is
```
git checkout <new_branch>
git rebase master
```

Remote git
======
###### Command to store the git repository to local
```
scp -r my_project.git user@git.example.com:/srv/git
```
