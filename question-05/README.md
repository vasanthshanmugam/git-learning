# Question 05: Default Branch in Git

## 📝 Question
What is the default branch in Git and how can it be changed?

## 🎯 Learning Objectives
By completing this exercise, you will understand:
- What a default branch is and why it matters
- Historical context: `master` vs `main`
- How to check your default branch
- How to change it globally and per-repository
- When and why to rename branches

## 🔍 Concept Overview

### What is a Default Branch?

The **default branch** is the branch Git creates automatically when you run `git init` or clone a repository.

**Historically:**
- Default was `master`
- First commit creates this branch

**Modern practice:**
- Many use `main` instead
- More inclusive terminology
- GitHub, GitLab changed defaults in 2020

**Why it matters:**
- Your starting point for all work
- Often the "production" or "stable" branch
- Where pull requests typically merge

### Branch Names Are Just Labels

Remember: Branch names are arbitrary! Git doesn't care if you use:
- `master`, `main`, `trunk`, `dev`, `production`
- The name you choose is just a convention

## 💻 Hands-On Exercise

### Setup: Create a New Practice Folder

```bash
# Navigate to Desktop or Documents
cd ~/Desktop

# Create practice folder
mkdir branch-practice
cd branch-practice
```

### Task 1: Check Your Current Default

Before initializing, check your global Git config:

```bash
git config --global init.defaultBranch
```

**Question:** What does it show? _________________

**If it shows nothing:** Your default is likely `master` (old default)

### Task 2: Initialize and See Default Branch

```bash
git init
```

**Question:** What branch name does Git mention? _________________

Check which branch you're on:

```bash
git branch
```

**Question:** Do you see any branches listed? _________________

**Why?** _________________

Make your first commit to create the branch:

```bash
echo "Initial file" > readme.txt
git add readme.txt
git commit -m "Initial commit"
```

Now check again:

```bash
git branch
```

**Question:** What branch appears now? _________________

**Question:** Is there an asterisk (*) next to it? What does that mean? _________________

### Task 3: Check Default Branch Configuration

View your Git configuration:

```bash
# Check local config (this repo only)
git config --local init.defaultBranch

# Check global config (all new repos)
git config --global init.defaultBranch

# Check system config (all users)
git config --system init.defaultBranch
```

**Question:** Which level has a value set? _________________

### Task 4: Change Default Branch Globally

Set your global default to `main`:

```bash
git config --global init.defaultBranch main
```

Verify it worked:

```bash
git config --global init.defaultBranch
```

**Question:** What does it show now? _________________

### Task 5: Test the New Default

Create another test repository:

```bash
cd ~/Desktop
mkdir test-default-branch
cd test-default-branch
git init
```

**Question:** What branch name does Git mention now? _________________

Make a commit:

```bash
echo "Test" > test.txt
git add test.txt
git commit -m "Test commit"
git branch
```

**Question:** What branch was created? _________________

**Success!** Your new default is working.

### Task 6: Rename an Existing Branch

Go back to your first practice folder:

```bash
cd ~/Desktop/branch-practice
git branch
```

Let's rename the current branch:

```bash
git branch -m main
```

**Note:** `-m` means "move/rename"

Check the result:

```bash
git branch
```

**Question:** What's the branch name now? _________________

Verify HEAD updated:

```bash
cat .git/HEAD
```

**Question:** What does HEAD point to now? _________________

### Task 7: Rename from a Different Branch

Create a new branch and switch to it:

```bash
git checkout -b feature
```

Now rename the `main` branch while on `feature`:

```bash
git branch -m main trunk
```

Check all branches:

```bash
git branch
```

**Question:** What branches exist now? _________________

**Question:** Which branch are you currently on? _________________

Switch back:

```bash
git checkout trunk
```

### Task 8: Understanding Default vs Current Branch

Create a new repo with your new default:

```bash
cd ~/Desktop
mkdir understanding-defaults
cd understanding-defaults
git init
```

**Question:** What's your default branch? _________________

Create a different branch:

```bash
git checkout -b develop
echo "Dev work" > dev.txt
git add dev.txt
git commit -m "Dev commit"
```

**Question:** What's your CURRENT branch? _________________

**Question:** What's your DEFAULT branch (the one git init created)? _________________

**Understanding:** 
- **Default branch** = What `git init` creates
- **Current branch** = Where HEAD points now (can be different!)

## ✅ Check Your Understanding

### Question 1: Does changing the global default affect existing repositories?

Test it:
```bash
# You already have branch-practice with 'main'
cd ~/Desktop/branch-practice
git branch

# Change global default to 'trunk'
git config --global init.defaultBranch trunk

# Check branch-practice again
git branch
```

**Answer:** _________________

### Question 2: What happens if you rename a branch that's pushed to GitHub?

**Think about it:**
- You rename `master` to `main` locally
- Your GitHub repo still has `master`
- What issues might this cause?

**Answer:** _________________

### Question 3: Can you have different default branches for different repositories?

**Answer:** _________________

**How would you do this?** _________________

### Question 4: What's the difference between these commands?

```bash
git branch -m new-name              # Command A
git config init.defaultBranch new-name   # Command B
```

**Answer:** _________________

## 🎓 Challenge Exercises

### Challenge 1: Set Different Defaults at Different Levels

```bash
# Set system-wide default (might need sudo)
git config --system init.defaultBranch system-branch

# Set global default
git config --global init.defaultBranch global-branch

# Create a repo and set local default
mkdir test-levels && cd test-levels
git init
git config --local init.defaultBranch local-branch

# Which one wins?
git config init.defaultBranch
```

**Question:** Which level takes precedence? _________________

### Challenge 2: Migrate a Project from master to main

```bash
# Create a repo with commits on master
cd ~/Desktop
mkdir migration-test
cd migration-test
git init
git config init.defaultBranch master  # Force old default
rm -rf .git && git init  # Reinitialize

echo "File 1" > file1.txt
git add file1.txt
git commit -m "Commit 1"

echo "File 2" > file2.txt
git add file2.txt
git commit -m "Commit 2"

git branch  # Should show master

# Now migrate to main
git branch -m master main
git branch

# Verify history is intact
git log --oneline
```

**Question:** Did you lose any commits? _________________

### Challenge 3: Understand Default Branch in Cloning

If you have a GitHub account:

```bash
# Clone a repository
git clone https://github.com/torvalds/linux.git linux-clone
cd linux-clone
git branch

# What's the default branch?
```

**Question:** What determines the default branch when cloning? _________________

**Answer:** The remote repository's default, NOT your local config!

## 📚 Solution

Ready to check your work? See [SOLUTION.md](./SOLUTION.md)

## 🔗 Next Steps
Once you understand default branches, move to [Question 06: Purpose of .git Directory](../question-06/)

---

## 💡 Quick Reference

### Check Default Branch
```bash
git config init.defaultBranch              # Current setting
git config --global init.defaultBranch     # Global setting
```

### Set Default Branch
```bash
git config --global init.defaultBranch main    # For all new repos
```

### Rename Current Branch
```bash
git branch -m new-name                     # Rename current branch
git branch -m old-name new-name           # Rename any branch
```

### See All Branches
```bash
git branch                                 # List local branches
git branch -a                              # Include remote branches
```
