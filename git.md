# Git & GitHub

**Git** is a Version Control System that runs locally on your machine. No need of internet to use it. **GitHub** is a service that hosts Git repositories in the cloud and makes it easier to collaborate with other people. Online place to share works that is done using Git.

` git status ` provides the status of the git repo.

` git init ` create an empty repository or re-initializes an existing repository.

` git add file1 file2 ` adds the specific files to the staging area from the working directory

` git commit -m ` is a checkpoint in time. A snapshot of changes. Commits changes from staging area to repository. The **` -m `** flag allows us to pass in an inline commit message, rather than launching a text editor

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


