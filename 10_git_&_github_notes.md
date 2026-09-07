## Git & GitHub 
### 1. Core Concepts & Architecture
#### What is Git?
Git is a distributed version control system (DVCS) that tracks changes in source code during software development. Unlike centralized systems, every developer's machine holds a full copy of the project repository and its historical commits.

#### What is GitHub? 
GitHub is a cloud-based hosting platform for Git repositories. It provides continuous integration/continuous deployment (CI/CD), issue tracking, code reviews (Pull Requests), and team collaboration features.

#### Git Architecture & Area Workflow
Git tracks files across four primary states/areas:
``` text
[ Working Directory ] --( git add )--> [ Staging Area (Index) ] --( git commit )--> [ Local Repository ] --( git push )--> [ Remote Repository (GitHub) ]
```
###### 1. Working Directory: The local file tree on your file system where you edit code.
###### 2. Staging Area (Index): A draft zone where file modifications are gathered before being recorded to history.
###### 3. Local Repository (.git directory): The local snapshot database containing all committed changes and history.
###### 4. Remote Repository: The hosted version of your repository on GitHub.

### 2. Initial Setup & Configuration
Configure your identity globally on your machine before creating commits.
Bash
###### Set global username
git config --global user.name "Your Name"

###### Set global email (should match your GitHub email)
git config --global user.email "your.email@example.com"

###### Set the default primary branch name to 'main'
git config --global init.defaultBranch main

###### Verify current configuration
git config --list


### 3. Basic Local Git Workflow
Initializing and Tracking Files
Bash
###### Initialize a new Git repository in the current folder
git init

###### Check the current status of files (untracked, modified, staged)
git status

###### Stage a specific file
git add index.html

###### Stage all .html file in the current directory excluding deleted ones
git add *.html

###### Stage only new or modified files, excluding deleted ones.
git add *

###### Stage all changes (new, modified, deleted) across the entire project.
git add --all | git add -A

###### Stage all changes (new, modified, deleted) in the current directory and everythin inside it.
git add .

###### Remove everything from the staging area and return them to the working directory
git reset

###### Commit staged changes with a concise message
git commit -m "feat: initial project setup and add index.html"

###### undo the last Commit and bring everything back to the working directory
git reset HEAD~

###### brings back the stage changes not acutal deleted files.
git reset

######  brings back both the stage changes and the acutal deleted files.
git reset --hard

###### remove four.txt and automatically move that change to the staging area
git rm four.txt

###### remove file only from the staging area both keep it physically in the working directory
git rm --cached four.txt

###### completely removes file
git rm --force four.txt | git rm -f four.txt

###### completely removes FOLDER and everything inside
git rm -f <FOLDER>

###### View commit history
git log

###### View compact, single-line commit history
git log --oneline --graph --all

### 4. Branching and Merging
Branches allow you to isolate feature development, bug fixes, or experiments without affecting the production branch (main). 
``` text
(feature/login)  A ─── B ─── C
                          /             \
(main)  X ───────────────Y───────────────Z  (Merged)
```

### Branch Management Commands
Bash
###### List all local branches
git branch

###### Create a new branch
git branch feature/user-auth

###### Switch to the new branch
git checkout feature/user-auth

###### Create and switch to a new branch in one command
git checkout -b feature/dashboard
###### OR (modern syntax)
git switch -c feature/dashboard

###### Merge changes from feature branch into the active branch
git checkout main
git merge feature/dashboard

###### Delete a local branch after merging
git branch -d feature/dashboard

###### Force delete an unmerged branch
git branch -D feature/dashboard

### Handling Merge Conflicts
A merge conflict occurs when Git cannot automatically reconcile differences between two commits on the same line of a file.

1. Run 'git status' to identify conflicted files.
2. Open the files and inspect conflict markers:
```text
Code snippet
<<<<<<< HEAD
Current branch changes
=======
Incoming branch changes
>>>>>>> feature-branch
```
3. Edit the file to preserve the correct code and remove conflict markers.
4. Stage the resolved file: git add <filename>
5. Finalize the merge commit: git commit -m "fix: resolve merge conflict"

### 5. Working with GitHub (Remotes)
Connecting Local and Remote Repositories
Bash
##### Link a local repository to a remote GitHub repository
git remote add origin https://github.com/username/repository-name.git

##### Verify remote configuration
git remote -v

##### Rename the default branch to main (if necessary)
git branch -M main

##### Push local commits to remote for the first time (-u sets upstream tracking)
git push -u origin main

##### Subsequent pushes
git push

##### Download changes and history from remote without merging
git fetch origin

##### Download and automatically merge remote changes into current branch
git pull origin main

###### help revert any file or directory back to its previous state of last commit. 
###### use to undo local uncommited changes, or removes changes that were added to the staging area using git add
git restore filename.extension | git restore directory_name

###### undo all changes across the entire repository
git restore .

###### remove files from the stagging area but keep the working directory unchanged
git restore --staged filename | git restore --staged .

### Cloning an Existing Repository
Bash
##### Clone a repository onto your local machine
git clone https://github.com/username/repository-name.git

###### temporarily set aside your unfinished workd in one branch, swithed to another branch to do something
git stash 

###### restore the stash changes back to your working directory, and remove the changes from stash list
git stash pop

###### restore the newsest stash changes back to your working directory, but keep the changes in the stash list.
git stash apply

##### Git can store a list of multiple stashes. And we can view all those stash list. To see the list run:
git stash list

###### remove a specific stash from a stash list
git stash drop

###### used to undo the changes made in a previous commit, but instead of deleting that old commit, it creates a new one that reverses those changes
git revert 'commit_id'

###### bringing updates from main branch into a another branch without merging, to got a clean commit history.
git rebase main

### 6. GitHub Collaboration Workflow
1. Forking: Copying another user's remote repository to your personal GitHub account.
2. Feature Branching: Creating a dedicated branch for each isolated unit of work (git checkout -b feature/xyz).
3. Pull Requests (PR): Submitting your branch changes on GitHub to request review and merging into the parent repository's main branch.
4. Code Review: Teammates comment, request modifications, or approve the PR.
5. Merge: Merging the approved PR into the base branch and deleting the topic branch.

### 7. Essential Git Inspection & Undo Tools
|  Action  |  Command  | Scope / Notes |
| :--- | :--- | :--- |
| Inspect Line Differences | git diff | Shows unstaged changes relative to the index. |
| Inspect Staged Differences | git diff --staged | Shows staged changes relative to HEAD. |
| Unstage a File | git restore --staged <file> | Moves file out of staging area; preserves workspace modifications. |
| Discard Local Changes | git restore <file> | Overwrites local modifications back to last commit state. |
| Soft Reset | git reset --soft HEAD~1 | Undoes the last commit; preserves changes in Staging. |
| Mixed Reset | git reset --mixed HEAD~1 | Undoes commit and un-stages changes; leaves code in Working Directory. |
|Hard Reset | git reset --hard HEAD~1 | Destructive: Completely deletes commit and changes. |
| Safety Net (Revert) | git revert <commit-hash> | Creates a new commit that reverses changes from a prior commit. Safe for public remotes. |

### 8. Best Practices & The .gitignore File
**.gitignore** Pattern Rules
Create a file named **.gitignore** at the root of your project to tell Git which files/directories to ignore (e.g., build artifacts, sensitive keys, environment variables).

Code snippet
###### Dependencies
node_modules/
vendor/

###### Environment Variables & Secrets
.env
.env.local

###### OS Generated Files
.DS_Store
Thumbs.db

###### Build Artifacts
dist/
build/
*.log

### Git Commit Guidelines
1. Commit Often: Make small, logical commits rather than large, monolithic ones.
2. Write Clear Commit Messages: Use imperative tense in the title line (e.g., "Add user login endpoints" instead of "Added user login endpoints").
3. Never Commit Secrets: Keep API keys, private passwords, and credentials out of Git history. If committed accidentally, purge using history-rewriting tools (e.g., git-filter-repo) and rotate credentials immediately.
