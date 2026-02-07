# Solution: Default Branch in Git

## ✅ Answers to Exercise Questions

### Task 1: Check Your Current Default

**Question:** What does it show?
- **Possible answers:**
  - **Nothing (blank)** - Using Git's built-in default (`master`)
  - **`main`** - You or your system already configured it
  - **Other name** - Custom configuration

### Task 2: Initialize and See Default Branch

**Question:** What branch name does Git mention?
- **Answer:** Depends on your config
  - `master` (if no global config set)
  - `main` (if you previously configured it)

**Question:** Do you see any branches listed?
- **Answer:** No! The list is empty

**Why?**
- Branches don't exist until you make a commit
- `git init` sets up the infrastructure, but no commits = no branches yet
- HEAD points to a branch that doesn't exist yet

**Question:** What branch appears now?
- **Answer:** Your default branch (master or main)

**Question:** Is there an asterisk (*) next to it? What does that mean?
- **Answer:** Yes, there's an asterisk
- **Meaning:** This is your CURRENT branch (where HEAD points)

### Task 3: Check Default Branch Configuration

**Question:** Which level has a value set?
- **Answer:** Typically `--global` if you've configured it
- **Hierarchy:** local > global > system
- **Local** overrides **global**, which overrides **system**

### Task 4: Change Default Branch Globally

**Question:** What does it show now?
- **Answer:** `main`
- This affects all NEW repositories you create

### Task 5: Test the New Default

**Question:** What branch name does Git mention now?
- **Answer:** `main`
- Because you changed the global default

**Question:** What branch was created?
- **Answer:** `main`
- Your new default is working!

### Task 6: Rename an Existing Branch

**Question:** What's the branch name now?
- **Answer:** `main`
- `git branch -m main` renamed your current branch

**Question:** What does HEAD point to now?
- **Answer:** `ref: refs/heads/main`
- HEAD automatically updated to track the renamed branch

### Task 7: Rename from a Different Branch

**Question:** What branches exist now?
- **Answer:** `feature` and `trunk`
- `main` was renamed to `trunk`

**Question:** Which branch are you currently on?
- **Answer:** `feature` (has the asterisk)
- You can rename branches even when not on them

### Task 8: Understanding Default vs Current Branch

**Question:** What's your default branch?
- **Answer:** `main` (what `git init` created)

**Question:** What's your CURRENT branch?
- **Answer:** `develop`

**Question:** What's your DEFAULT branch?
- **Answer:** Still `main` (the original)

**Understanding:**
- Creating a new branch doesn't change what the default branch is
- Default branch = the first branch created by `git init`
- Current branch = where you are now (can be anywhere)

## ✅ Check Your Understanding - Answers

### Question 1: Does changing the global default affect existing repositories?

**Answer:** NO!

**Explanation:**
- Global default only affects NEW repositories created after the change
- Existing repositories keep their current branches
- To change existing repos, you must rename branches manually with `git branch -m`

**Example:**
```
Before config change:
- Repo A has 'master'

After: git config --global init.defaultBranch main

Repo A still has 'master' (unchanged)
New repos get 'main'
```

### Question 2: What happens if you rename a branch that's pushed to GitHub?

**Answer:** You create a mismatch between local and remote!

**Problems:**
- Local has `main`, remote has `master`
- `git push` might fail or create a new branch
- Collaborators still see `master` as default
- Pull requests target the old branch

**Proper migration steps:**
1. Rename locally: `git branch -m master main`
2. Push new branch: `git push -u origin main`
3. Change default on GitHub (Settings → Branches)
4. Delete old branch: `git push origin --delete master`
5. Tell teammates to update their local repos

### Question 3: Can you have different default branches for different repositories?

**Answer:** Yes!

**How:**
Use local configuration instead of global:

```bash
cd my-repo
git config --local init.defaultBranch custom-branch
```

**But note:**
- This only affects `git init` if you reinitialize (rare)
- More commonly, you just create/rename branches as needed
- Each repo can have different branch names independently

### Question 4: What's the difference between these commands?

**Command A:** `git branch -m new-name`
- Renames an EXISTING branch
- Changes the current branch name right now
- Immediate effect on this repository

**Command B:** `git config init.defaultBranch new-name`
- Sets the default for FUTURE repositories
- Doesn't change any existing branches
- Only affects new `git init` operations

**Summary:**
- A = Rename existing branch NOW
- B = Configure default for LATER

## 🎓 Challenge Exercises - Solutions

### Challenge 1: Set Different Defaults at Different Levels

**Question:** Which level takes precedence?

**Answer:** Local > Global > System

**Precedence order:**
1. **Local** (`.git/config`) - Highest priority
2. **Global** (`~/.gitconfig`) - Medium priority  
3. **System** (`/etc/gitconfig`) - Lowest priority

If local is set, it wins. If not, global wins. If neither, system wins.

**Test result:**
```bash
git config init.defaultBranch
# Returns: local-branch
```

### Challenge 2: Migrate a Project from master to main

**Question:** Did you lose any commits?

**Answer:** NO! All commits are preserved.

**Explanation:**
- Branch names are just labels pointing to commits
- Renaming a branch only changes the label
- The commit history remains intact
- Git log shows the same commits before and after

**Visual:**
```
Before:
master → commit2 → commit1

After:
main → commit2 → commit1

Same commits, different label!
```

### Challenge 3: Understand Default Branch in Cloning

**Question:** What determines the default branch when cloning?

**Answer:** The REMOTE repository's default branch!

**Explanation:**
- Your local `init.defaultBranch` config doesn't matter
- When cloning, Git uses whatever the remote has set as default
- Most GitHub/GitLab repos now default to `main`
- Older repos might still use `master`

**To check remote's default:**
```bash
git remote show origin
# Look for "HEAD branch:"
```

## 🔑 Key Takeaways

### 1. Default Branch Basics

**Definition:** The first branch created when you run `git init`

**Historical Default:** `master`

**Modern Default:** `main` (many organizations switched in 2020)

### 2. How to Change Default

**For all new repositories:**
```bash
git config --global init.defaultBranch main
```

**For specific repository:**
```bash
git config --local init.defaultBranch custom
```

### 3. Renaming Branches

**Rename current branch:**
```bash
git branch -m new-name
```

**Rename any branch:**
```bash
git branch -m old-name new-name
```

**What gets updated:**
- Branch reference in `.git/refs/heads/`
- HEAD (if you're on that branch)
- Working directory (if you're on that branch)

### 4. Configuration Levels

Git has 3 configuration levels:

| Level | File | Scope | Priority |
|-------|------|-------|----------|
| System | `/etc/gitconfig` | All users | Lowest |
| Global | `~/.gitconfig` | Your user | Medium |
| Local | `.git/config` | This repo | Highest |

### 5. Master vs Main

**Why the change?**
- More inclusive language
- "Master" has historical problematic connotations
- "Main" is neutral and clear

**What hasn't changed:**
- Git functionality is identical
- Branch names are arbitrary
- You can use any name you want

### 6. Important Points

**Changing default doesn't affect:**
- Existing repositories
- Remote repositories
- Cloned repositories

**You need to:**
- Rename branches manually in existing repos
- Update remote defaults separately
- Communicate changes to your team

## 📊 Visual Summary

### Configuration Hierarchy
```
Local Config (.git/config)
        ↓ (overrides)
Global Config (~/.gitconfig)
        ↓ (overrides)
System Config (/etc/gitconfig)
```

### Default Branch Timeline
```
Before git init:
- No repository
- No branches

git init:
- Creates .git folder
- Sets up default branch name
- But branch doesn't exist yet!

First commit:
- Default branch is created
- HEAD points to it
- Now you can see it with git branch
```

### Renaming Flow
```
Before: master → commit3 → commit2 → commit1
                  ↑
                 HEAD

Rename: git branch -m main

After:  main → commit3 → commit2 → commit1
                ↑
               HEAD

Same commits, different name!
```

## 🔧 Common Commands Reference

### Check Current Settings
```bash
# View default branch setting
git config init.defaultBranch

# View all config levels
git config --list --show-origin | grep defaultBranch
```

### Set Default Branch
```bash
# Set globally (recommended)
git config --global init.defaultBranch main

# Set locally (specific repo)
git config init.defaultBranch main

# Unset (revert to Git's default)
git config --global --unset init.defaultBranch
```

### Rename Branches
```bash
# Rename current branch
git branch -m new-name

# Rename specific branch
git branch -m old-name new-name

# Force rename (use with caution)
git branch -M new-name
```

### Check Branches
```bash
# List local branches
git branch

# Show current branch name only
git branch --show-current

# List all branches (including remote)
git branch -a
```

## 🚀 Real-World Scenarios

### Scenario 1: New Project
```bash
git config --global init.defaultBranch main
mkdir my-project
cd my-project
git init
# Creates 'main' branch automatically
```

### Scenario 2: Existing Project Migration
```bash
cd existing-project
git branch  # Currently on 'master'
git branch -m main
git push -u origin main
# Update GitHub default branch in settings
git push origin --delete master
```

### Scenario 3: Team Migration
```bash
# 1. Team lead announces migration
# 2. Everyone updates global config
git config --global init.defaultBranch main

# 3. For existing projects:
git branch -m master main
git fetch origin
git branch -u origin/main main
git remote set-head origin -a
```

## 🚀 What's Next?

Now you understand how default branches work and how to configure them!

Continue to [Question 06: Purpose of .git Directory](../question-06/)
