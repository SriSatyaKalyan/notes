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

***Ignoring Files***: 
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

***Merging***: We have to remember two things:
* We merge branches, not specific commits
* We always merge to the current HEAD branch

To merge, follow the basic steps:
1. Switch to or checkout the branch you want to merge the changes into (the receiving branch)
2. Using the **` git merge `** command to merge changes from a specific branch into the current branch

This is called a fast-forward merge. This can be performed when there is a direct linear path from the source branch to the target branch. In a fast-forward merge, git simply moves the source branch pointer to the target branch pointer without creating an extra merge commit.

When we try to merge our branch into a master which has other *` non-conflicting `* changes added to it, git performs a **` merge commit `** wherein we end up with a new commit on the master branch. Git will prompt you for a message.

***Resolving Conflicts***: Whenever you encounter merge conflicts, follow the below steps:
1. Open up the file(s) with merge conflicts
2. Edit the file(s) to remove the conflicts. Decide which branch's content you want to keep in each conflicts. Or keep the content from both.
3. Remove the conflict "markers" in the document
4. Add your changes and then make a commit!

The content from the branch you are trying to merge from is displayed **` between the ======= and >>>>>>> symbols`**. 

` git diff ` command is used to view changes between commits, branches, files, working directory, etc. We often use this alongside other commands like ` git status ` and ` git log `, to get a better picture of a repo and how it has changed over time.

Without additional options, ` git diff ` lists all the changes in our working directory that are NOT staged for the next commit. Shows ***unstaged*** changes.

` git diff HEAD ` lists ***ALL*** changes in the working tree since your last commit. Shows ***changed*** and ***unchanged*** changes since HEAD.

` git diff --staged ` or ` git diff --cached ` will list the changes between the staging area and our last commit. (Shows what will be included in the commit if ` git commit ` command is ran right now)

```
git diff + git diff --staged = git diff HEAD
```

` git diff HEAD [filename] ` and ` git diff --staged [filename] ` will be Diff-ing specific files .

` git diff [branch1] [branch2] ` will list the changes between the tips of the branch1 and branch2. The order matters.

***Stashing***: Git provides an easy way of stashing these uncommitted changes so that we can return to them later, without having to make unnecessary commits.

` git stash ` (or ` git stash save `) will take all uncommitted changes (staged and unstaged) and stash them, reverting the changes in your working copy.

` git stash pop ` command is used to remove the most recently stashed changes in your stash and re-apply them to your working copy. The stash is cleared here. 

` git stash apply ` command applies to the current branch whatever is stashed away, without removing it from the stash. This can be useful if you want to apply stashed changes to multiple branches. The stash still has the changes.

**Stashing Multiple Times**: One can add multiple stashes into the stack of stashes. They will all be stashed in the order that they have been added.

` git stash list ` command lists the order in which the stashes have been performed. ` git stash apply stash@{[number_of_stash]}` applies the stash which has numbered. 

` git drop stash@{2} ` deletes the stash numbered 2. ` git stash clear ` clears out all the stashes. 

***Undoing Changes & Time Traveling***: 

` git checkout commit <commit-hash>` command is used to view a previous commit. ` git switch master ` takes us back to where the HEAD used to be.

` git checkout ` supports a syntax for referencing previous commits relative to a HEAD or a particular commit. 
* ***HEAD~1*** refers to the commit before HEAD (parent)
* ***HEAD~2*** refers to 2 commits before HEAD (grandparent)

` git switch - ` will take us whichever branch which we were on before we switched HEAD to.

***Discarding Changes***: 
` git checkout HEAD <filename> ` is used to discard any changes in that file, reverting back to the HEAD. Another way of achieving the same result is by using the ` git checkout -- <filename> ` command.

` git restore ` command is used to undoing changes. ` git restore ` and ` git switch ` are used as alternatives to some of the uses of ` checkout `.

To restore the file to the contents in the HEAD, we use `git restore <filename> `. ` git restore --source HEAD~1 <filename> ` will restore the contents of the file to its state from the commit prior to HEAD. We can also a particular commit hash as the source. 

NOTE: The above command is not "undoable". If we have uncommitted changes in the file, they will be lost!

***Unstaging Files with Restore***: If we have accidentally added a file to the staging area with ` git add ` command but we don't wish to include it in the next commit, we can use ` git restore ` to remove it from staging. 
The command would be ` git restore --staged <filename> `.

` git reset <commit-hash> ` command will reset the repo back to a specific commit. The commits are gone but the changes made during those commits stay. 

` git reset --hard <commit-hash> ` is a hard reset command which will delete the commit and also undo the changes made starting from that commit.

` git revert ` is similar to ` git reset ` in that they both "undo" changes, but they accomplish it in different ways. ` git reset ` actually moves the branch pointer backwards, eliminating the commits. ` git revert ` instead creates a brand new commit which reverses/undoes the changes from a commit. Because it results in a new commit, a prompt requesitng a commit message has to be handled.

` git revert ` is used when we want to reverse some commits that other people already have on their machines. 