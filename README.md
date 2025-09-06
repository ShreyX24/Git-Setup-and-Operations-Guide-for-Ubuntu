# Git Setup and Operations Guide for Ubuntu

## Table of Contents
1. [Initial Git Setup with SSH](#initial-git-setup-with-ssh)
2. [Working with Your Own Repository](#working-with-your-own-repository)
3. [Working with Someone Else's Repository](#working-with-someone-elses-repository)
4. [Common Git Operations](#common-git-operations)
5. [Troubleshooting](#troubleshooting)

---

## Initial Git Setup with SSH

### Step 1: Generate SSH Key
```bash
ssh-keygen -t ed25519 -C "your.email@gmail.com"
```
- Press Enter to accept default file location
- Optionally set a passphrase (recommended for security)

### Step 2: Add SSH Key to GitHub
```bash
cat ~/.ssh/id_ed25519.pub
```
- Copy the entire output
- Go to GitHub → Settings → SSH and GPG keys → New SSH key
- Paste the key and give it a descriptive title
- Click "Add SSH key"

### Step 3: Test SSH Connection
```bash
ssh -T git@github.com
```
You should see: `Hi USERNAME! You've successfully authenticated...`

---

## Working with Your Own Repository

### Scenario 1: Existing Repository (Clone and Work)
```bash
# Clone your repository
git clone git@github.com:USERNAME/REPOSITORY.git
cd REPOSITORY

# Make changes, then commit and push
git add .
git commit -m "Your commit message"
git push origin main
```

### Scenario 2: Existing Local Project (Add Remote)
```bash
# If you already have a local project
cd your-project-directory

# Initialize git (if not already done)
git init

# Add remote repository
git remote add origin git@github.com:USERNAME/REPOSITORY.git

# Set upstream and push
git branch -M main
git push -u origin main
```

### Scenario 3: Change Existing HTTPS to SSH
```bash
# Check current remote
git remote -v

# Change to SSH
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git

# Verify change
git remote -v

# Now you can push normally
git push origin main
```

---

## Working with Someone Else's Repository

### Step 1: Fork the Repository
- Go to the original repository on GitHub
- Click the "Fork" button (top-right)
- This creates a copy in your GitHub account

### Step 2: Clone Your Fork
```bash
git clone git@github.com:YOUR_USERNAME/REPOSITORY.git
cd REPOSITORY
```

### Step 3: Add Upstream Remote
```bash
# Add the original repository as upstream
git remote add upstream git@github.com:ORIGINAL_OWNER/REPOSITORY.git

# Verify remotes
git remote -v
# Should show:
# origin    git@github.com:YOUR_USERNAME/REPOSITORY.git (fetch)
# origin    git@github.com:YOUR_USERNAME/REPOSITORY.git (push)
# upstream  git@github.com:ORIGINAL_OWNER/REPOSITORY.git (fetch)
# upstream  git@github.com:ORIGINAL_OWNER/REPOSITORY.git (push)
```

### Step 4: Create Feature Branch
```bash
# Always create a new branch for your changes
git checkout -b feature/your-feature-name

# Or for bug fixes
git checkout -b fix/bug-description
```

### Step 5: Make Changes and Commit
```bash
git add .
git commit -m "Descriptive commit message"
```

### Step 6: Keep Your Fork Updated
```bash
# Fetch latest changes from original repository
git fetch upstream

# Switch to main branch
git checkout main

# Merge upstream changes
git merge upstream/main

# Push updates to your fork
git push origin main
```

### Step 7: Push Your Feature Branch
```bash
# Push your feature branch to your fork
git push origin feature/your-feature-name
```

### Step 8: Create Pull Request
- Go to your fork on GitHub
- Click "Compare & pull request"
- Fill in the PR description
- Submit the pull request

---

## Common Git Operations

### Checking Status and History
```bash
# Check current status
git status

# View commit history
git log --oneline

# View remotes
git remote -v

# Check current branch
git branch
```

### Branch Operations
```bash
# Create and switch to new branch
git checkout -b branch-name

# Switch between branches
git checkout branch-name

# List all branches
git branch -a

# Delete local branch
git branch -d branch-name

# Delete remote branch
git push origin --delete branch-name
```

### Syncing with Remote
```bash
# Fetch changes without merging
git fetch origin

# Pull changes (fetch + merge)
git pull origin main

# Push changes
git push origin branch-name
```

---

## Troubleshooting

### Authentication Issues
If you get authentication errors:
```bash
# Test SSH connection
ssh -T git@github.com

# If using HTTPS, switch to SSH
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```

### Permission Denied (publickey)
```bash
# Check if SSH agent is running
eval "$(ssh-agent -s)"

# Add your SSH key
ssh-add ~/.ssh/id_ed25519

# Test connection again
ssh -T git@github.com
```

### Merge Conflicts
```bash
# When conflicts occur during merge/pull
git status  # Shows conflicted files

# Edit conflicted files manually, then:
git add conflicted-file.txt
git commit -m "Resolve merge conflict"
```

### Reset Changes
```bash
# Discard unstaged changes
git checkout -- filename

# Discard all unstaged changes
git checkout -- .

# Reset to last commit (careful!)
git reset --hard HEAD
```

---

## Best Practices

1. **Always work on feature branches** when contributing to others' repositories
2. **Keep your fork updated** with the upstream repository
3. **Write descriptive commit messages**
4. **Test your changes** before pushing
5. **Use SSH over HTTPS** for better security and convenience
6. **Create meaningful pull requests** with proper descriptions

---

## Quick Reference Commands

```bash
# Setup
ssh-keygen -t ed25519 -C "email@gmail.com"
cat ~/.ssh/id_ed25519.pub

# Own repo
git clone git@github.com:USERNAME/REPO.git
git remote set-url origin git@github.com:USERNAME/REPO.git

# Others' repo
git clone git@github.com:YOUR_USERNAME/FORKED_REPO.git
git remote add upstream git@github.com:ORIGINAL_OWNER/REPO.git
git checkout -b feature/new-feature

# Daily workflow
git add .
git commit -m "message"
git push origin branch-name
```
