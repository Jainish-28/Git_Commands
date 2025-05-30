# Complete Git Commands Reference & Workflow Guide

## Table of Contents
1. [Basic Setup](#basic-setup)
2. [Repository Operations](#repository-operations)
3. [File Operations](#file-operations)
4. [Commit Operations](#commit-operations)
5. [Branch Operations](#branch-operations)
6. [Remote Operations](#remote-operations)
7. [Viewing & Inspecting](#viewing--inspecting)
8. [Undoing Changes](#undoing-changes)
9. [Git Workflow](#git-workflow)
10. [Advanced Commands](#advanced-commands)
11. [Best Practices](#best-practices)

---

## Basic Setup

### Initial Configuration
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main
git config --list                    # View all configurations
```

### Authentication Setup
```bash
git config --global credential.helper store    # Store credentials
ssh-keygen -t rsa -b 4096 -C "your.email@example.com"    # Generate SSH key
```

---

## Repository Operations

### Creating & Cloning
```bash
git init                            # Initialize new repository
git clone <url>                     # Clone remote repository
git clone <url> <directory>         # Clone to specific directory
git clone --depth 1 <url>          # Shallow clone (latest commit only)
```

---

## File Operations

### Staging Files
```bash
git add <file>                      # Stage specific file
git add .                           # Stage all changes
git add *.js                        # Stage all JS files
git add -A                          # Stage all changes (including deletions)
git add -u                          # Stage modified/deleted files only
```

### Unstaging Files
```bash
git reset <file>                    # Unstage specific file
git reset                           # Unstage all files
```

### File Status
```bash
git status                          # Show working directory status
git status -s                       # Short status format
git diff                            # Show unstaged changes
git diff --staged                   # Show staged changes
```

---

## Commit Operations

### Creating Commits
```bash
git commit -m "Commit message"      # Commit with message
git commit -am "Message"            # Stage and commit all changes
git commit --amend                  # Modify last commit
git commit --amend -m "New message" # Change last commit message
```

### Commit History
```bash
git log                             # View commit history
git log --oneline                   # Compact log format
git log --graph                     # Show branch graph
git log --author="Name"             # Filter by author
git log -n 5                        # Show last 5 commits
git log --since="2 weeks ago"       # Time-based filtering
```

---

## Branch Operations

### Creating & Switching Branches
```bash
git branch                          # List local branches
git branch -a                       # List all branches (local + remote)
git branch <branch-name>            # Create new branch
git checkout <branch-name>          # Switch to branch
git checkout -b <branch-name>       # Create and switch to new branch
git switch <branch-name>            # Modern way to switch branches
git switch -c <branch-name>         # Create and switch (modern)
```

### Branch Management
```bash
git branch -d <branch-name>         # Delete branch (safe)
git branch -D <branch-name>         # Force delete branch
git branch -m <old> <new>           # Rename branch
git branch --merged                 # Show merged branches
git branch --no-merged              # Show unmerged branches
```

### Merging
```bash
git merge <branch-name>             # Merge branch into current
git merge --no-ff <branch>          # Force merge commit
git merge --squash <branch>         # Squash merge
```

---

## Remote Operations

### Remote Management
```bash
git remote                          # List remotes
git remote -v                       # List remotes with URLs
git remote add <name> <url>         # Add remote
git remote remove <name>            # Remove remote
git remote rename <old> <new>       # Rename remote
```

### Fetching & Pulling
```bash
git fetch                           # Fetch from default remote
git fetch <remote>                  # Fetch from specific remote
git fetch --all                     # Fetch from all remotes
git pull                            # Fetch and merge
git pull --rebase                   # Fetch and rebase
git pull origin <branch>            # Pull specific branch
```

### Pushing
```bash
git push                            # Push to default remote
git push origin <branch>            # Push to specific branch
git push -u origin <branch>         # Push and set upstream
git push --all                      # Push all branches
git push --tags                     # Push all tags
git push --force                    # Force push (use carefully!)
```

---

## Viewing & Inspecting

### File Content
```bash
git show <commit>                   # Show commit details
git show <commit>:<file>            # Show file at specific commit
git blame <file>                    # Show line-by-line history
git annotate <file>                 # Alternative to blame
```

### Differences
```bash
git diff <file>                     # Changes in working directory
git diff --staged <file>            # Changes in staging area
git diff <commit1> <commit2>        # Compare commits
git diff <branch1>..<branch2>       # Compare branches
```

### Search
```bash
git grep "search term"              # Search in tracked files
git log --grep="pattern"            # Search commit messages
git log -S "code"                   # Search for code changes
```

---

## Undoing Changes

### Working Directory
```bash
git checkout -- <file>              # Discard changes in file
git checkout .                      # Discard all changes
git clean -f                        # Remove untracked files
git clean -fd                       # Remove untracked files and directories
```

### Staging Area
```bash
git reset <file>                    # Unstage file
git reset                           # Unstage all files
git reset --hard                    # Reset to last commit (destructive)
```

### Commits
```bash
git revert <commit>                 # Create new commit that undoes changes
git reset --soft HEAD~1             # Undo last commit, keep changes staged
git reset --mixed HEAD~1            # Undo last commit, keep changes unstaged
git reset --hard HEAD~1             # Undo last commit, discard changes
```

### Advanced Undos
```bash
git reflog                          # Show reference log
git reset --hard <commit>           # Reset to specific commit
git cherry-pick <commit>            # Apply specific commit
```

---

## Git Workflow

### Standard Workflow
```
1. Clone repository:     git clone <url>
2. Create feature branch: git checkout -b feature/new-feature
3. Make changes and stage: git add .
4. Commit changes:       git commit -m "Add new feature"
5. Push to remote:       git push -u origin feature/new-feature
6. Create Pull Request (on GitHub/GitLab)
7. Merge and delete branch
```

### Gitflow Workflow
```
Main branches:
- main/master: Production-ready code
- develop: Integration branch

Supporting branches:
- feature/*: New features
- release/*: Release preparation
- hotfix/*: Production fixes
```

### Feature Branch Workflow
```bash
# Start new feature
git checkout -b feature/user-authentication
git push -u origin feature/user-authentication

# Work on feature
git add .
git commit -m "Implement login functionality"
git push

# Keep up to date with main
git checkout main
git pull origin main
git checkout feature/user-authentication
git merge main

# Finish feature (create PR/MR)
```

---

## Advanced Commands

### Stashing
```bash
git stash                           # Stash current changes
git stash push -m "Work in progress" # Stash with message
git stash list                      # List all stashes
git stash pop                       # Apply and remove latest stash
git stash apply                     # Apply stash without removing
git stash drop                      # Delete latest stash
git stash clear                     # Delete all stashes
```

### Rebasing
```bash
git rebase <branch>                 # Rebase current branch
git rebase -i HEAD~3                # Interactive rebase (last 3 commits)
git rebase --continue               # Continue after resolving conflicts
git rebase --abort                  # Cancel rebase
```

### Tags
```bash
git tag                             # List tags
git tag <tag-name>                  # Create lightweight tag
git tag -a <tag-name> -m "Message"  # Create annotated tag
git tag -d <tag-name>               # Delete tag
git push origin <tag-name>          # Push tag to remote
git push origin --tags              # Push all tags
```

### Submodules
```bash
git submodule add <url> <path>      # Add submodule
git submodule init                  # Initialize submodules
git submodule update                # Update submodules
git submodule update --remote       # Update to latest remote
```

---

## Best Practices

### Commit Messages
```
Format: <type>(<scope>): <description>

Types:
- feat: New feature
- fix: Bug fix
- docs: Documentation
- style: Formatting
- refactor: Code restructuring
- test: Adding tests
- chore: Maintenance

Examples:
feat(auth): add user login functionality
fix(api): resolve null pointer exception
docs(readme): update installation instructions
```

### Branch Naming
```
feature/feature-name
bugfix/bug-description
hotfix/critical-fix
release/version-number
experiment/new-idea
```

### General Tips
- Commit early and often
- Write meaningful commit messages
- Use branches for features
- Keep commits atomic (one logical change)
- Pull before pushing
- Review changes before committing
- Use .gitignore for unwanted files
- Regular backups with remotes

### Common .gitignore Patterns
```
# Dependencies
node_modules/
vendor/

# Build outputs
dist/
build/
*.o
*.class

# Environment files
.env
.env.local

# IDE files
.vscode/
.idea/
*.swp

# OS files
.DS_Store
Thumbs.db
```

---

## Troubleshooting

### Common Issues
```bash
# Merge conflicts
git status                          # See conflicted files
# Edit files to resolve conflicts
git add <resolved-files>
git commit

# Detached HEAD
git checkout <branch-name>          # Return to branch

# Accidentally committed to wrong branch
git log --oneline -n 5              # Find commit hash
git checkout <correct-branch>
git cherry-pick <commit-hash>
git checkout <wrong-branch>
git reset --hard HEAD~1

# Remove sensitive data
git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch <file>' \
--prune-empty --tag-name-filter cat -- --all
```

### Useful Aliases
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
```

---

*This guide covers the most essential Git commands and workflows. Keep it handy for quick reference!*
