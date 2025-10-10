# Git Commands Cheat Sheet 📚

## Table of Contents
- [Setup & Configuration](#setup--configuration)
- [Getting & Creating Projects](#getting--creating-projects)
- [Basic Snapshotting](#basic-snapshotting)
- [Undoing Changes](#undoing-changes)
- [Branching & Merging](#branching--merging)
- [Collaboration](#collaboration)
- [Inspection & Comparison](#inspection--comparison)
- [Stashing & Cleaning](#stashing--cleaning)
- [Tags & Releases](#tags--releases)
- [Advanced Manipulation](#advanced-manipulation)
- [Useful References](#useful-references)

---

## Setup & Configuration

<details>
<summary>Click to expand Setup & Configuration commands</summary>

### Configure Git globally
```bash
# Set username globally for commits
git config --global user.name "Your Name"

# Set email globally for commits
git config --global user.email "your@email.com"

# View current configuration
git config --global --list

# Set default branch name
git config --global init.defaultBranch main

# Set default editor
git config --global core.editor "code --wait"
```

### Additional Configuration
```bash
# Check specific config value
git config user.name

# Set config for current repository only
git config user.name "Project Specific Name"

# Remove a config setting
git config --global --unset user.name
```

</details>

---

## Getting & Creating Projects

<details>
<summary>Click to expand Getting & Creating Projects commands</summary>

### Initialize and Clone
```bash
# Initialize a local repository
git init

# Initialize with specific branch name
git init -b main

# Clone a remote repository
git clone <repo_url>

# Clone to a specific directory
git clone <repo_url> <directory_name>

# Clone only the latest commit (shallow clone)
git clone --depth 1 <repo_url>
```

### Remote Management
```bash
# Add a remote (GitHub, GitLab, etc)
git remote add origin <url>

# View remote repositories
git remote -v

# Change remote URL
git remote set-url origin <new_url>

# Remove a remote
git remote remove origin
```

</details>

---

## Basic Snapshotting

<details>
<summary>Click to expand Basic Snapshotting commands</summary>

### Checking Status and Staging
```bash
# List files to be committed
git status

# Short status format
git status -s

# Stage a specific file for commit
git add <filename>

# Stage all files
git add .

# Stage all files with specific extension
git add *.js

# Interactive staging
git add -i
```

### Committing Changes
```bash
# Commit staged changes
git commit -m "Your message"

# Commit all changes (skip staging)
git commit -a -m "Your message"

# Edit last commit message
git commit --amend

# Commit with multiline message
git commit -m "Title" -m "Description"
```

</details>

---

## Undoing Changes

<details>
<summary>Click to expand Undoing Changes commands</summary>

### File Level Changes
```bash
# Discard changes in a specific file
git checkout -- <filename>

# Restore file to last committed state
git restore <filename>

# Remove file from repository
git rm <filename>

# Remove file from staging area only
git rm --cached <filename>
```

### Commit Level Changes
```bash
# Reset all changes back to last commit
git reset --hard HEAD

# Reset to specific commit
git reset --hard <commit_id>

# Soft reset (keep changes in staging)
git reset --soft HEAD~1

# Make a new commit that undoes a previous one
git revert <commit_id>
```

</details>

---

## Branching & Merging

<details>
<summary>Click to expand Branching & Merging commands</summary>

### Branch Management
```bash
# List all branches
git branch

# List remote branches
git branch -r

# List all branches (local and remote)
git branch -a

# Create a new branch
git branch <branchname>

# Delete a branch
git branch -d <branchname>

# Force delete a branch
git branch -D <branchname>
```

### Switching Branches
```bash
# Create and switch to a new branch
git checkout -b <branchname>

# Switch to existing branch
git checkout <branchname>

# Switch to previous branch
git checkout -

# Create branch from specific commit
git checkout -b <branchname> <commit_id>
```

### Merging
```bash
# Merge branch into current branch
git merge <branchname>

# Merge with no fast-forward
git merge --no-ff <branchname>

# Abort a merge
git merge --abort

# Delete a remote branch
git push origin --delete <branchname>
```

</details>

---

## Collaboration

<details>
<summary>Click to expand Collaboration commands</summary>

### Push Changes
```bash
# Upload changes to remote repository
git push

# Push a branch to remote
git push origin <branchname>

# Push and set upstream
git push -u origin <branchname>

# Force push (use with caution)
git push --force

# Push tags
git push --tags
```

### Pull Changes
```bash
# Fetch and merge changes from remote repo
git pull

# Pull from specific branch
git pull origin <branchname>

# Pull with rebase
git pull --rebase

# Fetch new data without merging
git fetch

# Fetch from all remotes
git fetch --all
```

</details>

---

## Inspection & Comparison

<details>
<summary>Click to expand Inspection & Comparison commands</summary>

### Log and History
```bash
# Show commit history
git log

# Brief log format
git log --oneline

# Show graph of commits
git log --graph --oneline --all

# Show commits by author
git log --author="Author Name"

# Show commits in date range
git log --since="2 weeks ago" --until="1 week ago"
```

### Show Changes
```bash
# Show what changed in a commit
git show <commit_id>

# Show changes not yet staged
git diff

# Show staged changes
git diff --staged

# Show changes between branches
git diff <source_branch> <target_branch>

# Show changes between commits
git diff <commit1> <commit2>
```

### File History
```bash
# Show file change history
git log -p <filename>

# Show who changed what in a file
git blame <filename>

# Show file at specific commit
git show <commit_id>:<filename>
```

</details>

---

## Stashing & Cleaning

<details>
<summary>Click to expand Stashing & Cleaning commands</summary>

### Stashing
```bash
# Save dirty work and clean working directory
git stash

# Stash with message
git stash save "Work in progress"

# List all stashes
git stash list

# Apply most recent stash
git stash apply

# Apply specific stash
git stash apply stash@{2}

# Pop (apply and remove) stash
git stash pop

# Remove all stashed entries
git stash clear

# Drop specific stash
git stash drop stash@{1}
```

### Cleaning
```bash
# Remove untracked files from working directory
git clean -f

# Remove untracked files and directories
git clean -fd

# Preview what will be cleaned
git clean -n

# Remove ignored files
git clean -fX
```

</details>

---

## Tags & Releases

<details>
<summary>Click to expand Tags & Releases commands</summary>

### Creating Tags
```bash
# Tag specific commits for release
git tag <tagname>

# Create annotated tag
git tag -a <tagname> -m "Release message"

# Tag specific commit
git tag -a <tagname> <commit_id> -m "Message"

# Create lightweight tag
git tag <tagname>
```

### Managing Tags
```bash
# List all tags
git tag

# List tags with pattern
git tag -l "v1.*"

# Show tag information
git show <tagname>

# Delete local tag
git tag -d <tagname>

# Delete remote tag
git push origin --delete <tagname>

# Push specific tag
git push origin <tagname>

# Push all tags
git push --tags
```

</details>

---

## Advanced Manipulation

<details>
<summary>Click to expand Advanced Manipulation commands</summary>

### Cherry Pick
```bash
# Apply changes from a specific commit
git cherry-pick <commit>

# Cherry pick multiple commits
git cherry-pick <commit1> <commit2>

# Cherry pick a range of commits
git cherry-pick <start_commit>..<end_commit>
```

### Rebase
```bash
# Apply commits from one branch onto another
git rebase <branch>

# Interactive rebase
git rebase -i HEAD~3

# Continue rebase after resolving conflicts
git rebase --continue

# Abort rebase
git rebase --abort
```

### Debugging
```bash
# Find commit that introduced a bug (binary search)
git bisect start
git bisect bad          # Current commit is bad
git bisect good <commit> # Known good commit
git bisect reset        # End bisect session

# Show the history of HEAD and branch references
git reflog

# Find when a file was deleted
git log --diff-filter=D --summary
```

### Advanced Operations
```bash
# Squash last 3 commits
git reset --soft HEAD~3
git commit -m "Squashed commits"

# Change author of last commit
git commit --amend --author="New Author <email@example.com>"

# Find commits that changed a specific line
git log -S "search_string" -p <filename>
```

</details>

---

## Useful References

### Documentation & Resources
- 📖 [Git Official Documentation](https://git-scm.com/doc)
- 📋 [Interactive Git Cheatsheet (PDF)](https://github.com/ravikant-diwakar/DevOps/blob/master/git-cheat-sheet-education.pdf)
- 🎓 [Pro Git Book (Free)](https://git-scm.com/book)
- 🛠️ [Git Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)

### Quick Tips
- Use `git help <command>` for detailed help on any command
- Use `git --version` to check your Git version
- Create aliases for frequently used commands: `git config --global alias.st status`
- Use `.gitignore` file to exclude files from version control

### Common Workflows
1. **Feature Branch Workflow**: Create feature branches, merge back to main
2. **Git Flow**: Use develop, feature, release, and hotfix branches
3. **GitHub Flow**: Simple workflow with feature branches and pull requests
4. **Forking Workflow**: Fork repository, make changes, create pull requests

---

## Emergency Commands 🚨

<details>
<summary>Click to expand Emergency Git Commands</summary>

```bash
# Undo last commit but keep changes
git reset --soft HEAD~1

# Completely undo last commit
git reset --hard HEAD~1

# Recover deleted branch
git checkout -b <branch_name> <commit_id>

# Find lost commits
git reflog
git checkout <commit_id>

# Force pull (overwrite local changes)
git fetch --all
git reset --hard origin/main

# Clean everything (DANGEROUS)
git clean -fd
git reset --hard HEAD
```

</details>

---
