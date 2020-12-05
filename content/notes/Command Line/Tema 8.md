---
title: 8. Git Repository
linktitle: 8. Git Repository
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Command Line
    weight: 8

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 8
---

Notes from the *Learn Git* course from Codecademy:

**Course Description**: Learn to save and manage different versions of your code projects with this essential tool.

**Course Certificate**
{{< figure library="true" src="git_course.jpg" >}}
The link: https://www.codecademy.com/profiles/netNinja82250/certificates/a8ab218d5950c29861635cc0bf12fd13



Git Repository
--------------

### 1. Basic Git Workflow
#### Checking the Status of a Git Repository
The git status command is used within a Git repository to its current status including the current commit, any modified files, and any new files not being tracked by Git.

The output of git status can vary widely, and it often includes helpful messages to direct the user to manage their repository. For example, git status will show the user the files they would commit by running git commit and the files they could commit by running git add before running git commit.

#### Initializing a Git Repository
The git init command creates or initializes a new Git project, or repository. It creates a .git folder with all the tools and data necessary to maintain versions. This command only needs to be used once per project to complete the initial setup. For instance, the code block sets up the home folder as a new git repository.

        $ cd /home
        $ git init

**git init** creates a new Git repository

#### Git Workflow
A Git project can be thought of as having three parts:

A Working Directory: where you’ll be doing all the work: creating, editing, deleting and organizing files
A Staging Area: where you’ll list changes you make to the working directory
A Repository: where Git permanently stores those changes as different versions of the project
The Git workflow consists of editing files in the working directory, adding files to the staging area, and saving changes to a Git repository. In Git, we save changes with a commit.

#### git status
As you write the screenplay, you will be changing the contents of the working directory. You can check the status of those changes with:

    git status

**git status** inspects the contents of the working directory and staging area

#### git add
We can add a file to the staging area with:

    git add filename

The word filename here refers to the name of the file you are editing.

**git add** adds files from the working directory to the staging area

#### git diff
We can check the differences between the working directory and the staging area with:

    it diff filename

**git diff** shows the difference between the working directory and the staging area

#### git commitA commit is the last step in our Git workflow. A commit permanently stores changes from the staging area inside the repository.

git commit is the command we’ll do next. However, one more bit of code is needed for a commit: the option -m followed by a message. Here’s an example:

    git commit -m "Complete first line of dialogue"

**git commit** permanently stores file changes from the staging area in the repository

Standard Conventions for Commit Messages:

* Must be in quotation marks
* Written in the present tense
* Should be brief (50 characters or less) when using -m

#### git log 
Often with Git, you’ll need to refer back to an earlier version of a project. Commits are stored chronologically in the repository and can be viewed with:

    git log

**git log** shows a list of all previous commits

### 2. How to Backtrack in Git

**git checkout HEAD filename**: Discards changes in the working directory.

**git reset HEAD filename**: Unstages file changes in the staging area.

**git reset commit_SHA**: Resets to a previous commit in your commit history.

### 3. Git Branching
Git branching allows users to experiment with different versions of a project by checking out separate branches to work on.

The following commands are useful in the Git branch workflow.

**git branch**: Lists all a Git project’s branches.

**git branch branch_name**: Creates a new branch.

**git checkout branch_name**: Used to switch from one branch to another.

**git merge branch_name**: Used to join file changes from one branch to another.

**git branch -d branch_name**: Deletes the branch specified.

### 4. Git Teamwork
The workflow for Git collaborations typically follows this order:

* Fetch and merge changes from the remote
* Create a branch to work on a new project feature
* Develop the feature on your branch and commit your work
* Fetch and merge from the remote again (in case new commits were made while you were working)
* Push your branch up to the remote for review

A remote is a Git repository that lives outside your Git project folder. Remotes can live on the web, on a shared network or even in a separate folder on your local computer. The Git Collaborative Workflow are steps that enable smooth project development when multiple collaborators are working on the same Git project.
We also learned the following commands

**git clone**: Creates a local copy of a remote.
**git remote -v**: Lists a Git project’s remotes.
**git fetch**: Fetches work from the remote into the local copy.
**git merge origin/master**: Merges origin/master into your local branch.
**git push origin <branch_name>**: Pushes a local branch to the origin remote.
