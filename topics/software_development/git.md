# Git

## Table of contents

+ [References](#references)
+ [Basics](#basics)
  + [Introduction](#introduction)
  + [Repository](#basics)
  + [Recordig changes](#basics)
  + [Undoing changes](#basics)
  + [Syncing repos](#basics)
  + [Managing history](#managing-history)
+ [Collaboration](#collaboration)
  +[Branches](#branches)
  +[Switching branches](#switching-branches)
  +[Remote branches](#remote-branches)
  +[Branching workflows](#branching-workflows)
  +[Integrating branches](#integrating-branches)
  +[Tagging](#tagging)
  +[Reviewing changes](#reviewing-changes)

## References

- [Beginner’s guide to Git](https://backlog.com/git-tutorial/)

Recommended:

- [Official webpage](https://git-scm.com/) (learn & download Git)
- [Official Documentation](https://git-scm.com/doc) (books, videos, links)
- [Brief Git and Github tutorial](https://www.youtube.com/watch?v=rWhnsx4PDQU&list=PLS1QulWo1RIZs8U9sZ8Xf-NNIzKJsu2jX)
- [Become a Git guru](https://www.atlassian.com/git/tutorials)
- [Udacity – Version control with Git](https://www.udacity.com/course/version-control-with-git--ud123)

## Basics

### Introduction

**Version Control System (VCS)**: It records and saves changes as you modify files, allowing to restore a previous version of your work at any time.

**Git**: Distributed VCS for managing source code. It's primarily command-line driven, though it offers GUIs. Main features:

- **Distributed**: Developers can work offline and independently on their own local copies.
- **Performance and efficiency**: It allows rapid branching, merging, and commiting changes, while handling large repositories and managing extensive version history.
- **Widely adopted**: It's the de facto standard VCS, and has a large community that offers support and guidance.
- **Tooling and integration**: It integrates with many development tools, text editors, IDEs, and some hosting platforms (like Backlog).

**Git architecture**: It's a three-tier architecture. Layers:

- **Working tree** (or **working directory**) (WT): It's where you make changes, the files you're working on (edit, add, and delete files). Changes here are "untracked" until explicitly added to the next layer (index).
- **Index** (or **staging area**): It's where the next commit is prepared. This ensures that only changes you want to include are committed. Files from the Working tree are compared to those in the repo, and modified files are marked as modified before committing them. This allows to review changes before committing and selectively stage parts of files.
- **Repository** (or **repo**): It's where the project's history is stored and all changes are tracked. It contains all the commits, branches, tags, and metadata. When you commit changes, they're moved from the Index to the Repo. Each commit represents a snapshot of the project at a given point in time.

**File states**:

- **Untracked**: A newly created file in the WT that has never been staged.
- **Modified**: Changes have been made to the file in the WT, but they have not been staged. 
- **Staged** (or **indexed**): The changes have been marked for inclusion in the next commit.
- **Committed**: The staged changes have been permanently recorded in the repository.

**Basic workflow**:

- **Initialize** a repository
- **Modify** files in the working tree
- **Stage** changes you want to include in the next commit
- **Commit** your changes and include a commit description
- Review the **history** of commits (`git log`)
- Use different **branches** to separate lines of development that diverge from the main project line.
- **Merge** your branch back into the main branch
- **Push** (share your changes) and **pull** (get updates from others) from remote

### Repository

**Repository**: Centrally located folder for storing files. You can track changes in the repository. Two repo types:

- **Remote**: Hosted on a remote (on Internet, off-site server, or same machine) and shared among multiple team members.
- **Local**: Hosted on a local machine for an individual user.

**Create repo**: Two options:

- **New repo** (`git init`): Starts with an empty history and no commits. Requires setup and configuration. Good for starting new projects.
- **Clone repo** (`git clone`): Copy an existing repo. Includes its entire commit history, branches, and files. By default, it sets up a local main branch that tracks the remote main branch it was cloned from. Good for joining ongoing projects.

### Recordig changes

You have to explicitly inform Git about the changes you want to track and record. By staging and commiting changes selectively, you get more control. You can commit specific files or even individual lines within a file. You make changes in the WT, then stage those changes you want to save in the index, and then make a commit. Only the changes staged in the index will be included in the commit and saved in the repo.

- **Commit**: Each commit creates a snapshot of changes made to the files since the last commit. It captures the project at a specific time that can be referenced, reverted to, or compared with other commits. Each commit is identified with a unique 40-character checksum hash. Best practices:

  - Separate different types of changes (bug fix, new feature, improvement…) into distinct commits.
  - Commit small, logical units.
  - Commit frequently, so each commit represents a manageable and coherent set of changes.
  - Review changes before committing: Review modified, added, or deleted files (`git status`), and see exact changes within files (`git diff`).
  - Stage changes selectively. Use `git add -p` to stage changes and commit only portions of a file. This keeps commits focuses and avoids including unnecessary changes.
  - Avoid committing large files or binaries: Git is optimized for text-based files, and large binaries can bloat the repo size and slow down operations. Use `.gitignore` files to exclude unnecessary files.
  - Use branches for feature development: This isolates work on new features or experimental changes. Merge branches into the main branch once changes are tested and complete.

**Commit message**: Each commit includes a message summarizing the committed changes concisely and accurately. Best practices:

- Keep messages consistent. Example: `<contents changed> <blank line> <reason for changes>`
- Subject line: Succinctly summarize the change.
- Body: Provide context and details.
- Separate subject from body with a blank line for readability.
- Start subject line with an imperative verb (add, fix, update…).
- Keep subject line under 50 characters for readability.
- Start subject line with a capital letter.
- Use bullet points in the body for complex changes
- Reference relevant issues (if the commit relates to a specific issue or task).
- Use Present tense for subject line, and Past tense for the body.

### Undoing changes

Main options:

- `git revert`: Undo previous commits (most commont method). It creates a new commit that reverts the changes made by a previous commit. It allows to undo changes without removing the commit and while preserving history.

- `git reset`: Delete previous commits from the history. It makes `HEAD` point to a previous commit. It's generally not recommended because it causes the remote repo to diverge from the local repos of other members (synchronization issues). It's used primarily to undo local commits that have not been yet pushed to a remote repo. It can permanently remove changes, so use with care. Reset modes:

  - `--soft`: Undoes a previous commit. Preserves changes in WT and index.
  - `--mixed` (default): Restores the state of a changed index. Preserves WT, resets index.
  - `--hard`: Removes all traces of a commit. Resets WT and index.

- `git rebase -i`: Rewrite commit history by opening an interactive editor where you can modify, reorder, squash, or delete specific commits before applying them to the current branch. Don't rebase commits that have already been pushed to a shared/public repo, as this creates diverget histories.

### Syncing repos

Remote repos can be on another computer or a private server. Ensure that your local repo is up-to-date with the remote repo and vice versa to share changes with other team members. Repos can be synced with:

- `git push` (upload): Send local commits to the remote repo (upload). This ensures the remote repo is up-to-date with the latest commits made by you (shares your work with others). Before pushing, it's good practice to pull the latest changes from remote to avoid conflict.
- `git pull` (download): Fetch and integrate changes from the remote repo into your local repo. This ensures your local copy is up-to-date with the latest commits made by other team members. Pulling involves two actions:
  - **Fetch**: Retrieves latest changes from remote but doesn't apply them to your WT.
  - **Merge**: Integrates the fetched changes into your local working branch, combining them with your existing changes.
- `git merge`: Combines changes from one branch into another (or the same). It identifies the common ancestor commit of both branches and combines the changes from the source branch into the target branch. You cannot push to the remote repo is your local repo is outdated; in this case you must merge the latest changes before pushing. If there's a conflict, an error will prompt you to resolve it manually.

**Merge conflict**: It happens when changes made in the local repo and the remote repo cannot be automatically reconciled by Git. Git will prompt you to resolve them by choosing which changes to keep or by manually editing the conflicting files. Git adds conflict-resolution markers to the conflicting file when this happens to show the sections that need to be resolved manually.

- Example: Two members make changes on the same part of a file in two different branches (i.e., remote and local branches).

```
<html>
 <head>
  <title>hello</title>
 </head>
 <body>
  <<<<<<<<<< HEAD
  Hello
  =======
  <strong>Hello</strong>
  >>>>>>>>>> 17c860612953c0f9d88f313c8dfbf7d858e02e91
 </body>
</html>
```

Everything above `=======` is your local contenct, and everything below comes from the remote branch. You must resolve the conflict before creating a merge commit:

```
<html>
 <head>
  <title>hello</title>
 </head>
 <body>
  <strong>Hello</strong>
 </body>
</html>
```

### Managing history

How to change your Git history before sharing your work with others.

**Amending a commit** (`git commit --amend`): Modify the most recent commit (change message, add new changes or remove changes from the commit, …). When to use: fixing mistakes in commit messages, adding forgotten changes, and remove unintended changes.

**Rebasing commits** (`git rebase -i`): Move or combine a sequence of commits to a new base commit. Useful for integrating changes from one branch (feature branch) into another (main branch) cleanly. When to use: updating a feature branch (that has fallen behind the main branch), cleaning up commit history (squash commits, reorder them, edit commit messages, create a more cohesive and readable commit history…), and avoiding merge commits (this applies changes directly to your branch).

- **Cherry-picking commits** (`git cherry-pick`): Apply a specific commit from one branch to another without merging the entire branch. Useful for selectively integrating changes without bringing in all the changes. When to use: applying specific changes, backporting fixes (apply a fix from a newer branch to an older release branch), applying specific critical updates.

- **Squashing commits** (`git merge --squash`): Combine multiple commits into a single commit. Useful for cleaning up and simplifying history. When to use: before merging, cleaning up history, improving commit messages, or preparing for review.

## Collaboration

### Branches

**Git branch**: Pointer to a specific commit in your repo's history. Independent line of development within a repository. Represents a snapshot of the project's files at a certain point in time. Separate branches can be merged into one branch. Changes in the primary of other branches will not affect your branch unless you pull the latest changes from those branches. It's common practice to create a new branch for each task (makes it easier to identify what changes to expect and simplifies backtracking).

**Benefits** of branches:

- **Isolation of work**: Developers can work independently without affecting the main codebase or developers (prevents interference).
- **Parallel development**: Teams can work concurrently on different tasks. Branches can evolve independently, and changes can be integrated later through merging or rebasing.
- **Feature development**: Branches are commonly used to develop new features (create feature branch > implement changes > test them > merge back into main branch).
- **Bug fixes**: Branches are also useful for isolating bug fixes (create branch > fix issue > test it > merge back into main branch).

**Branch creation** (`git branch <branch_name>`): This creates a separate line of development that diverges from the main codebase. When creating a branch, Git creates a pointer to a specific commit (HEAD of the branch). A branch can be named to identify its purpose. In a branch we can make changes and commits independently from other branches. The various commits we make in the branch form a chronological history of changes specific to that branch.

### Switching branches

**Switching branches** (`git checkout <branch>`): This updates the files (files, directories, and their contents) in your working tree (working directory) to match the latest commits (version) on the branch you're switching to. It's like switching between different workspaces. Git moves the HEAD pointer to point the latest commit of the branch you switched to. Committed changes in the previous branch will be hidden or replaced. If you have uncommitted changes (that conflict with the branch you're switching to), Git will prevent the switch until you either commit, stash, or discard those changes.

**Pointing to branches**: A branch is a pointer to a specific commit in your repo's history.

- **HEAD pointer**: Reference to the currently checked-out branch or the commit you're working on. When switching branches, Git moves `HEAD` to point to the latest commit of the new branch. It's used to represent the current snapshot of a branch. For a new repo, Git will point `HEAD` to the main branch by default. Changing where `HEAD` points will update your active branch.
  - `HEAD~<n>`: Refers to the ancestors (`HEAD~1` refers to the commit's first parent, `HEAD~2` refers its first grandparent, etc.).
  - `HEAD^<N>`: Refers to the parents of merge commits (`HEAD^1` refers to the first parent of `HEAD` where head is a merge commit, `HEAD^2` refers to the first grandparent of `HEAD` where head is a merge commit, etc.).
- **Branch pointer**: When creating a new branch, Git creates a new pointer that initially points to the same commit as the branch you created it from.
- **Commit history**: The commits form a linked list where each commit points to its parent commit/s. Branches are maintained by moving these pointers to different commits as new commits are made, effectively changing the state of the branch.
  
<br>![Usage of ~ and ^](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/git_1.png)

**Stashing branches**: Mechanism to save your changes temporarily. Stashing refers to temporarily shelving changes that you've made to your working directory so that you can work on something else, typically without committing those changes to your branch.

### Remote branches

### Branching workflows

### Integrating branches

### Tagging

### Reviewing changes