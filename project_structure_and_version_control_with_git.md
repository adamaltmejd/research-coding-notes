
# Git

Git is a version control system (VSC). We use it to keep track of progress and changes in our research projects and for collaboration. A *Git repository* is a directory that contains a hidden folder called `.git` where the VSC keeps track of everything. Github.com is a website where one can freely host Git repositories making it easy to collaborate. Git is extremely sophisticated with lots of useful functions but here we will focus on only the most important parts.

Essential for successfully working with Git is proper project compartmentalization. Make sure each git repository contains one research project that will result in one paper. It is better to reuse code across multiple repositories than to squish everything into one.

While Git is collaborative it is designed around each developer working on their own copy of the project. As a developer completes working on some specific functionality, fixes a bug or similar they commit the changes to git and include a commit message describing the change. The changes can then be pushed to the remote repository on e.g. Github where everyone else working on the code can download them.

## Git concepts

* **repository**: a project folder that is managed by git
* **commit**: to record code changes to the version control system, should include a message describing the changes/fix
* **branch**: a git repository can have multiple branches. The default branch is the *master* branch. If a developer wants to work on bigger changes including multiple commits and make sure that the main code base is not updated with changes that the other users are adding he/she can create a new branch, off master. When its finished, the changes can then be merged into master.
* **remote**: a server where a version of the repository is stored that all developers access, usually Github. It is to here that commits are pushed/pulled.
* **push/pull**: Push your own changes to the remote repository or pull other people's updates from remote to your own folder.
* **merge conflict**: Git automatically tries to merge changes in remote with your local code when pulling, or between two branches that are being merged. But sometimes this will not work and a merge conflict arises. In this situation the developer has to chose which code to keep and what to throw away.

## A collaborative git workflow



# Project folder structure

Here is a suggested project folder structure. I've made a script that can create a stucture like this for new projects that can be downloaded [https://github.com/adamaltmejd/research-project-template](here).
