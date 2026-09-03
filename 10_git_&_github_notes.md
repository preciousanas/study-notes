## Git & GitHub 
1. Core Concepts & Architecture
#### What is Git?
Git is a distributed version control system (DVCS) that tracks changes in source code during software development. Unlike centralized systems, every developer's machine holds a full copy of the project repository and its historical commits.

#### What is GitHub? 
GitHub is a cloud-based hosting platform for Git repositories. It provides continuous integration/continuous deployment (CI/CD), issue tracking, code reviews (Pull Requests), and team collaboration features.

#### Git Architecture & Area Workflow
Git tracks files across four primary states/areas:
```mermaid
flowchart LR
[ Working Directory ] ──( git add )──> [ Staging Area (Index) ] ──( git commit )──> [ Local Repository ] ──( git push )──> [ Remote Repository (GitHub) ]
```
Working Directory: The local file tree on your file system where you edit code.Staging Area (Index): A draft zone where file modifications are gathered before being recorded to history.Local Repository (.git directory): The local snapshot database containing all committed changes and history.Remote Repository: The hosted version of your repository on GitHub.2. Initial Setup & ConfigurationConfigure your identity globally on your machine before creating commits.Bash# Set global username
git config --global user.name "Your Name"

# Set global email (should match your GitHub email)
git config --global user.email "your.email@example.com"

# Set the default primary branch name to 'main'
git config --global init.defaultBranch main

# Verify current configuration
git config --list
3. Basic Local Git WorkflowInitializing and Tracking FilesBash# Initialize a new Git repository in the current folder
git init

# Check the current status of files (untracked, modified, staged)
git status

# Stage a specific file
git add index.html

# Stage all changes (new, modified, deleted) in the directory
git add .

# Commit staged changes with a concise message
git commit -m "feat: initial project setup and add index.html"

# View commit history
git log

# View compact, single-line commit history
git log --oneline --graph --all
4. Branching and MergingBranches allow you to isolate feature development, bug fixes, or experiments without affecting the production branch (main).          (feature/login)  A ─── B ─── C
                          /             \
(main)  X ───────────────Y───────────────Z  (Merged)
Branch Management CommandsBash# List all local branches
git branch

# Create a new branch
git branch feature/user-auth

# Switch to the new branch
git checkout feature/user-auth

# Create and switch to a new branch in one command
git checkout -b feature/dashboard
# OR (modern syntax)
git switch -c feature/dashboard

# Merge changes from feature branch into the active branch
git checkout main
git merge feature/dashboard

# Delete a local branch after merging
git branch -d feature/dashboard

# Force delete an unmerged branch
git branch -D feature/dashboard
Handling Merge ConflictsA merge conflict occurs when Git cannot automatically reconcile differences between two commits on the same line of a file.Run git status to identify conflicted files.Open the files and inspect conflict markers:Code snippet<<<<<<< HEAD
Current branch changes
=======
Incoming branch changes
>>>>>>> feature-branch
Edit the file to preserve the correct code and remove conflict markers.Stage the resolved file: git add <filename>Finalize the merge commit: git commit -m "fix: resolve merge conflict"5. Working with GitHub (Remotes)Connecting Local and Remote RepositoriesBash# Link a local repository to a remote GitHub repository
git remote add origin https://github.com/username/repository-name.git

# Verify remote configuration
git remote -v

# Rename the default branch to main (if necessary)
git branch -M main

# Push local commits to remote for the first time (-u sets upstream tracking)
git push -u origin main

# Subsequent pushes
git push

# Download changes and history from remote without merging
git fetch origin

# Download and automatically merge remote changes into current branch
git pull origin main
Cloning an Existing RepositoryBash# Clone a repository onto your local machine
git clone https://github.com/username/repository-name.git
6. GitHub Collaboration WorkflowForking: Copying another user's remote repository to your personal GitHub account.Feature Branching: Creating a dedicated branch for each isolated unit of work (git checkout -b feature/xyz).Pull Requests (PR): Submitting your branch changes on GitHub to request review and merging into the parent repository's main branch.Code Review: Teammates comment, request modifications, or approve the PR.Merge: Merging the approved PR into the base branch and deleting the topic branch.7. Essential Git Inspection & Undo ToolsActionCommandScope / NotesInspect Line Differencesgit diffShows unstaged changes relative to the index.Inspect Staged Differencesgit diff --stagedShows staged changes relative to HEAD.Unstage a Filegit restore --staged <file>Moves file out of staging area; preserves workspace modifications.Discard Local Changesgit restore <file>Overwrites local modifications back to last commit state.Soft Resetgit reset --soft HEAD~1Undoes the last commit; preserves changes in Staging.Mixed Resetgit reset --mixed HEAD~1Undoes commit and un-stages changes; leaves code in Working Directory.Hard Resetgit reset --hard HEAD~1Destructive: Completely deletes commit and changes.Safety Net (Revert)git revert <commit-hash>Creates a new commit that reverses changes from a prior commit. Safe for public remotes.8. Best Practices & The .gitignore File.gitignore Pattern RulesCreate a file named .gitignore at the root of your project to tell Git which files/directories to ignore (e.g., build artifacts, sensitive keys, environment variables).Code snippet# Dependencies
node_modules/
vendor/

# Environment Variables & Secrets
.env
.env.local

# OS Generated Files
.DS_Store
Thumbs.db

# Build Artifacts
dist/
build/
*.log
Git Commit GuidelinesCommit Often: Make small, logical commits rather than large, monolithic ones.Write Clear Commit Messages: Use imperative tense in the title line (e.g., "Add user login endpoints" instead of "Added user login endpoints").Never Commit Secrets: Keep API keys, private passwords, and credentials out of Git history. If committed accidentally, purge using history-rewriting tools (e.g., git-filter-repo) and rotate credentials immediately.
