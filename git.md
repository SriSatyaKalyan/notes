# Git & GitHub

***Git*** is a Version Control System that runs locally on your machine. No need of internet to use it. ***GitHub*** is a service that hosts Git repositories in the cloud and makes it easier to collaborate with other people. Online place to share works that is done using Git.

## Git

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

## GitHub

***Remote***: Before we can push anything to GitHub, we need to tell Git about our remote repository (destination) on Github which we need to setup. In Git, we refer to these "destinations" as remotes. Each remote is simply a URL where a hosted repository lives.

A remote is two things: URL and a label. To add a new remote, we need to provide both to Git. 
```
git remote add <label> <url> 
```

So, here we are associating the **` label `** with the **` url `**. And hereonwards, whenever we refer to the label, we are actually referring to the url

**`Origin`** is a conventional Git remote name, but it is not special. It's just a name for a URL. We can change it.

To rename a remote, ` git remote rename <old> <new> ` can be used. 
To delete a remote, ` git remote remove <name> `

Now, we understand better ` git push <remote> <branch> `. Here we are pushing the branch into the remote, and therefore, we are pushing the branch into the url associated with the remote.

While we often push our local branch up to a remote branch of the same name, we can also push different branches up. This is with the command
` git push <remote> <local-branch>:<remote-branch> ` 

To push our local pancake branch up to a remote branch called waffle, we could do: ` git push origin pancake:waffle `

**`-u`**: The ` -u ` allows us to set the **`upstream`** of the branch we're pushing. This can be thought of as a link connecting our local branch to a branch on Github. Running ` git push -u origin master ` sets the upstream of the local master branch so that it tracks the master branch on the origin repo. So, after setting this upstream, running `git push` in the master branch would push the changes up to the remote master branch

`git remote -v` command tells us which remote branches the local branch is **`fetch`**-ing from and **`push`**-ing into.

`git branch -r` lists the remote branches and points out which remote branch the HEAD is pointing to. 

**`Remote-tracking branches`** are references to the state of remote branches. They're local references that you can't move; Git moves them for you whenever you do any network communication, to make sure they accurately represent the state of the remote repository.
* They follow this pattern **`<remote>/<branch>`**
* **`origin/master`** references the state of the master branch on the remote repo named origin.

That is the reason we see the below reference to the remote-tracking branch as below when we make commits locally but have not pushed the changes to remote.
```
Your branch is ahead of 'origin/master' by 2 commits. (use git push to publish your local commits)
```

To understand how the project looked like when we last interacted with the remote, we use ` git checkout origin/master ` command

When we clone a git repo from Github which has multiple branches, we only get the reference to the origin/master remote. To access other branches, we can use ` git switch <remote-branch-name> ` which creates a new local branch from the remote branch of the same name. 

**`Fetching`** allows us to download changes from a remote repo to our local repo, BUT those changes will not be automatically integrated into our working files. It lets one see what others have been working on, without having to merge those changes into the local repo. 

`git fetch <remote>` command fetches branches and history from a specific remote repository. It only updates remote tracking branches. `git fetch origin` would fetch all changes from the origin remote repo. If not specified as in the command `git fetch`, `<remote>` defaults to `origin`.

`git pull <remote> <master>` would fetch the latest information from the origin's master branch and merge those changes into our current branch. Just like `git merge`, it matters WHERE we run this command from. Whatever branch we run it from is where the changes will be merged into.

```
git pull = git fetch + git merge
```

If we run `git pull` without specifying a particular remote or branch to pull from, git assumes the following:
* remote will default to origin
* branch will default to whatever tracking connection is configured for your current branch


| git fetch      | git pull |
| ---        |    --- |
| Gets changes from remote branch(es)  | Gets changes from remote branch(es) |
| Updates the remote tracking branches with the new changes   | Updates the current branch with the new changes, merging them in         |
| Does not merge changes onto your current HEAD branch   | Can result in merge conflicts  |
| Safe to do anytime | Not recommended if you have uncommitted changes         |
|  |  |

**`README`** If you put README in the root of your project, Github will recognize it and automatically display it on the repo's home page. These are Markdown files, ending with the .md extension.

**`GITHUB Gists`** are a simple way to share code snippets and useful fragments wit others. Gists are much easier to create, but offer far fewer features than a typical Github repository.

**`Github Pages`** is a hosting service for static webpages, so it deos not support server-side code like Python, Ruby, or Node. Just HTML/CSS/JS.
* **User site** We get one user site per Github account. This is where we can host a portfolio site or some form of personal website. The default url is based on our Github username, following the pattern `username.github.io` though we can change this
* **Project site** We get unlimited project sites. Each Github repo can have a corresponding hosted website. It's as simple as telling Github which specific branch contains the web content. The default urls follow the pattern `username.github.io/repo-name`

### Workflows:

**Centralized Workflow** Everyone works on the master/main branch aka the most basic workflow possible. The simples collaborative workflow is to have everyone work on the master branch (or main, or any other SINGLE branch)

**Feature Branches** Rather than working on master/main, all new development should be done on separate branches!
* Treat master/main branch as the official project history
* Multiple teammates can collaborate on a single feature and share code back and forth without polluting the main branch
* Main branch won't contain broken code (unless someone messes up)

**`Pull Requests`** allow developers to alert team-members to new work that needs to be reviewed. They provide a mechanism to approve or reject the work on a given branch. They also help facilitate discussion and feedback on specific commits. 

#### Workflow
1. Do some work locally on a feature branch
2. Push up the feature branch on Github
3. Open a pull request using the featuer branch just pushed up to Github
4. Wait for PR to be approved and merged. Start a discussion on PR (depending on team structure)

* Switch to the branch in question. Merge in master and resolve the conflicts
```
> git fetch origin
> git switch my-new-feature
> git merge master
fix conflicts!!
```

* Switch to master. Merge in the feature branch (now with no conflicts). Push changes up to Github
```
> git switch master
> git merge my-new-feature
> git push origin master
```

* **Deleting** the remote does **NOT** delete the local branch.

**Fork & Clone** Instead of just one centralized Github repo, every developer has their own Github repo in addition to the "main" repo. Developers make changes and push to their own forks before making pull requests. (Commonly used on large open-source projects where there may be thousands of contributors with only a couple of maintainers)

*Fork* When we fork a repo, we are basically asking Github "Make me an own copy of this repo". 

So, the workflow would be as shown in the below steps:
1. FORK the project
2. Clone the Fork
3. Add upstream remote
4. Do some work
5. Push to origin
6. Open PR

This workflow might be complicated, but it's common for a good reason. It allows project maintainers to accept contributions from developers all around the world without having to add them as actual owners of the main project repo or worry about giving them all permissions to push to the repo.

### Rebasing

There are two main ways to use the `git rebase` command:
- as an alternative to merging
- as a cleanup tool

Instead of having a bunch of merge commits, we can instead rebase the feature branch onto the master branch. This moves the entire feature branch so that it BEGINS at the tip of the master branch. All of the work is still there, but we have **re-written history**

Instead of using a merge commit which adds additional merge-commit information, rebasing re-writes history by **creating new commits** for each of the original feature branch commits.

```
> git switch feature
> git rebase master
```

`git rebase master` would mean that we are re-basing the branch we are in onto the master branch

**When to Rebase** 
* We get a much cleaner project history
* No unnecessary merge commits!
* We end up with a linear project history

**When NOT to Rebase** 

Never rebase commits that have been shared with others. If you have already pushed commits up to Github, **DO NOT** rebase them unless you are positive no one on the team is using those commits

After addressing the conflicts, and finishing up making the changes, we can run ` git rebase --continue `

### Interactive Rebasing

Running `git rebase` with the `-i` option will enter the interactive mode, which allows us to edit commits, add files, drop commits, etc. Note that we need to specify how far back we want to rewrite commits.

```
git rebase -i HEAD~4
```

Also, notice that we are not rebasing onto another branch. Instead, we are rebasing a series of commits onto the HEAD they are currently based on.

In our text editor, we'll see a list of commits alongside a list of commands that we can choose from. Here are a couple of more commonly used commands:
* pick - use the commit
* reword - use the commit, but edit the commit message
* edit - use commit, but stop for amending
* fixup - use commit contents but meld it into previous commit and discard the commit message
* drop - remove commit

## Tags

Tags are pointers that refer to particular points in Git history. We can mark a particular moment in time with a tag. Tags are most often used to mark vesion releases in projects (v4.1.0, v4.1.1, etc.)

Think of tags as branch references that do not change. Once a tag is created, it always referes to the same commit. It is just a label for a commit.

There are two types of Git tags we can use: 
* **lightweight** tags are  lightweight. They are just a name/label that points to a particular commit
* **annotated** tags store extra meta data including the author's name and email, date and a tagging message (like a commit message) 

To create a lightweight tag, use `git tag <tagname>`. By default, Git will create the tag referring to the commit that HEAD is referencing.

To create an annotate tage, use `git tag -a`. Git will open default text editor and prompt us for additional information. Similar to git commit, we can use the `-m` option to pass a message directly and forgo the opening of the text editor.

**Semantic Versioning** spec outlines a standardized versioning system for software releases. It provides a consistent way for developers to give meaning to their software releases (how big of a change is this release?). Version consist of three numbers separated by periods.

```
2.4.1 
* 2 - MAJOR Release
* 4 - MINOR Release
* 1 - PATCH Release
```

Typically, the first release is 1.0.0

**Patch Release** (0.0.1) normally does not contain new features or significant changes. They typically signify bug fixes and other changes that do not impact how the code is used

**Minor Release** (1.1.0) signify that new features or functionality have been added, but the project is still backwards compatible. No breaking changes. The new functionality is optional and should not force users to rewrite their own code. Whenever there is a minor release, the patch release number gets reset to 0.

**Major Release** signify significant changes that is no longer backwards compatible. Features may be removed or changed substantially. Whenever there is a major release, the minor and patch release numbers gets reset to 0.

`git tag` will print a list of all the tags in the current repository. Type `q` to exit.

We can search for tags that match a particular pattern by using `git tag -l` and then passing in a wildcard pattern. For example, `git tag -l "*beta*"` will print a list of tags that include "beta" in their name.

***Checking Out Tags*** To view the state of a repo at a particular tag, we can use `git checkout <tag>`. This puts us in detached HEAD!

`git diff <tag1> <tag2>` compares the repo state in between the tags.

`git show <tag>` provides information about a tag.

We can tag older commits by providing a commit hash: 
`git tag -a <tagname> <commit-hash>`

Git will yell at us if we try to reuse a tag that is already referring to a commit. If we use the `-f` option, we can FORCE our tag through: `git tag -f <tagname> <commit-hash>`

To delete a tag, use `git tag -d <tagname>`

By default, `git push` command does not transfer tags to remote servers. If we want to push our tags at once, we can use the `--tags` option to the push command. This will transfer all our tags to the remote server that are not already there.
`git push --tags`

### Config

The config file is for  configuration. In this, we can configure things on a per-repo basis. 

### Refs Folder

Inside of refs, we will find a heads directory. **refs/heads** contains one file per branch in a repository. Each file is named after a branch and contains the hash of the commit at the tip of the branch. For example, **refs/heads/master** contains the commit hash of the last commit on the master branch. Refs also contains a **refs/tags** folder which contains one file for each tag in the repo.

### HEAD

HEAD is just a text file that keeps track of where HEAD points. If it contains *refs/heads/master*, this means that HEAD is pointing to the master branch

In detached HEAD, the HEAD file contains a commit hash instead of a branch reference

### Objects Folder

The objects directory contains all the repo files. This is where Git stores the backups of files, the commits in a repo, and more. The files are all compressed and encrypted.

#### Hashing
Hashing functions map input data of some arbitrary size to fixed-size output values.

### Blobs
Git blobs (binary large objects) are the object type Git uses to store the **contents of files** in a given repo. Blobs don't even include the filenames of each file or any other data. They just store the contents of a file.

### Trees
Trees are Git objects used to store the contents of a directory. Each tree contains pointers that can refer to blobs and to other trees. Each entry in a tre contains the SHA-1 hash of a blob or tree, as well as the mode, type and filename

### Commits
Commit objects combine a tree object along with information about the context that led to the current tree. Commits store a reference to parent commit(s), the author, the commiter, and the commit message.

When we run git commit, Git creates a new commit object whose parent is the **current HEAD commit** and whose tree is the current content of the index.

`git cat-file -t <commit-hash>` gives us the object type the commit is referring to.

`git cat-file -p <commit-hash>` gives us the pretty-printed version of the contents of the object the commit is referring to.

### Annotated Tags
Annotated tags contain metadata, commit message and pointers towards commits, which in turn reference towards trees, which in turn reference blobs

## Reflogs
Git keeps a record of when tips of branches and other references were updated in the repo. We can view and update these reference logs using the `git reflog` command

Git only keeps reflogs on your local activity. They are not shared with collaborators. Reflogs also expire. Git cleans out old entries after around 90 days, though this can be configured.

The git reflog command accepts subcommands **show**, **expire**, **delete**, and **exists**. Show is the only commonly used variant, and it is the default subcommand. 

`git reflog show` will show the log of a specific reference (it defaults to HEAD). For example, to view the logs for the tip of the main branch, we could run `git reflog show main`

**Reflog References** We can access specific git refs using `name@{qualifier}`. We can use this syntax to access soecific ref pointers and can pass them to other commands including checkout, reset and merge.

**Timed References** Every entry in the reference logs has a timestamp associated with it. We can filter reflogs entries by time/date by using time qualifiers like:
* 1.day.ago
* 3.minutes.ago
* yesterday
* Fri, 12 Feb 2021 14:0:21-0800

```
git reflog master@{one.week.ago}
git checkout bugfix@{2.days.ago}
git diff main@{0} main@{yesterday}
```
We can sometimes use reflog entries to access commits that seem lost and are not appearing in git log

### Related links
* https://gist.github.com/joseluisq/1e96c54fa4e1e5647940
* https://semver.org/