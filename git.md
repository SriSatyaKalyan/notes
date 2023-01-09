# Git & GitHub

**Git** is a Version Control System that runs locally on your machine. No need of internet to use it. **GitHub** is a service that hosts Git repositories in the cloud and makes it easier to collaborate with other people. Online place to share works that is done using Git.

` git status ` provides the status of the git repo.

` git init ` create an empty repository or re-initializes an existing repository.

` git add file1 file2 ` adds the specific files to the staging area from the working directory

` git commit -m ` is a checkpoint in time. A snapshot of changes. Commits changes from staging area to repository. The **` -m `** flag allows us to pass in an inline commit message, rather than launching a text editor

` git commit -a -m "commit_message" ` command adds the files and then commits them using the commit message in the quotes.

***Atomic Commits***: When possible, a commit should encompass a single feature, change, or fix. In other words, try to **` keep each commit focused on a single thing `**. This makes it much easier to undo or rollback changes later on. It also makes your code or project easier to review. 

Describe your changes in imperative/past mood and stick to it, e.g. **` "make child do sandcastle" `** instead of "This makes child do sandcastle". So, the commits should be as if orders are provided to the codebase to change its behavior.

` git log ` shows commit logs. ` git log --oneline ` shows commit made previously in one line format and easy to read and revise.

` git commit amend ` is used to redo the previous commit using the **` --amend `** option.

****Ignoring Files****: 
We can tell Git which files and directories to ignore in a given repository using a **` .gitignore `** file. This is useful for files/folders we never want to commit, including:
* Secrets, API keys, credentials, etc.
* Operating System files (.DS_Store on Mac)
* Log files
* Dependencies & packages

**` HEAD `**: HEAD is simply a pointer that refers to the current "location" in a repository. It points to a particular branch reference. HEAD generally points to the latest commit made on the master branch, but we can move around and HEAD will change.

` git branch <branch-name> ` is used to create a new branch based on the current HEAD. However, this does not switch us to the branch. So, the HEAD stays the same.

` git switch <branch-name> ` switches the HEAD to the branch that we have mentioned.

` git checkout <branch-name> ` command also switches branches. It also does other things like restoring working tree files.

` git switch -c <branch-name> ` command can be used to create a new branch with branch-name AND switch us over to the branch. Similarly, ` git checkout -b <branch-name> ` command can be used for the same purpose.

When switching branches with unstaged changes, git checks for the changes being in conflict with other branches and suggests to either commit/stash the changes accordingly when switching branches. 

` git branch -d <branch-name> ` command deletes a branch but checks if the changes made in the branch are merged. ` git branch -D <branch-name> ` command however deletes the branch irrespective of the changes being merged.

` git branch -m <new-branch-name> ` command helps us rename a branch. But we would have to switch to that branch first.



