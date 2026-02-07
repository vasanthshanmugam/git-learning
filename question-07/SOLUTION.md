# Solution: How Do You Check the Current Branch?

## ✅ Answers to Exercise Questions

### Task 1: Check Branch Before First Commit

**Question:** What do you see?
- **Answer:** Nothing! Empty list
- No branches are shown

**Why is the list empty?**
- **Answer:** Branches don't exist until the first commit
- `git init` sets up infrastructure but doesn't create branches yet

**Question:** What does it say about the branch?
- **Answer:** Something like "On branch master" (or "On branch main")
- Git knows the branch name but the branch doesn't exist yet

### Task 2: Create First Commit and Check Again

**Question:** What branch appears?
- **Answer:** `master` or `main` (depending on your default)

**Question:** Is there an asterisk (*) next to it?
- **Answer:** Yes!

**What does the asterisk mean?**
- **Answer:** This is your CURRENT branch
- The asterisk marks where HEAD is pointing

### Task 3: Multiple Ways to Check Current Branch

#### Method 1: git branch
**Output:** Shows all branches with * next to current

#### Method 2: git status
**Question:** Which line tells you the branch?
- **Answer:** First line: "On branch master" (or "On branch main")

#### Method 3: git branch --show-current
**Question:** What does this show?
- **Answer:** Just the branch name: `master` or `main`

**Question:** How is this different from `git branch`?
- **Answer:** 
  - `git branch` shows ALL branches
  - `git branch --show-current` shows ONLY current branch name
  - Useful for scripts

#### Method 4: Check HEAD file
**Question:** What does it say?
- **Answer:** `ref: refs/heads/master` (or `main`)

**Question:** Can you see the branch name in there?
- **Answer:** Yes! After `refs/heads/`

### Task 4: Create Multiple Branches and Practice

**Question:** How many branches do you see?
- **Answer:** 4 branches (master/main, feature, bugfix, experimental)

**Question:** Which one has the asterisk?
- **Answer:** `master` or `main` (whichever you started with)

**Question:** What does this tell you?
- **Answer:** You're still on the original branch
- Creating branches doesn't switch to them automatically

### Task 5: Switch Branches and Check

**Question:** Which branch has the asterisk now?
- **Answer:** `feature`

**Output:** (git branch --show-current)
- **Answer:** `feature`

**Output:** (after switching to bugfix)
- **Answer:** `bugfix`

### Task 6: See All Branches Including Remote

**Question:** How many branches are listed?
- **Answer:** 6 branches (master/main, feature, bugfix, experimental, dev, staging)

**Question:** Do you see any remote branches?
- **Answer:** No (unless you've set up a remote)
- Remote branches appear as `remotes/origin/branch-name`

### Task 7: Verbose Branch Information

**Question:** What extra information does this show?
- **Answer:** 
  - Commit hash (shortened)
  - Commit message

**Question:** Does it show commit hashes?
- **Answer:** Yes! First 7 characters of the commit hash

Example output:
```
* master  a1b2c3d Initial commit
  feature a1b2c3d Initial commit
  bugfix  a1b2c3d Initial commit
```

### Task 8: Current Branch in Different Scenarios

#### Scenario A
**Question:** Are you on new-feature?
- **Answer:** NO!

**Why/why not?**
- **Answer:** `git branch new-feature` only CREATES the branch
- It doesn't switch to it
- You're still on your previous branch

#### Scenario B
**Question:** Now are you on new-feature?
- **Answer:** YES!

#### Scenario C
**Question:** What branch are you on?
- **Answer:** `quick-feature`

**What did `git checkout -b` do?**
- **Answer:** Two things:
  1. Created the branch
  2. Switched to it

### Task 9: Understanding Branch Output Colors

**Question:** What color is the current branch?
- **Answer:** Green (in most terminals)

**Question:** What color are other branches?
- **Answer:** White/default terminal color

### Task 10: Programmatic Branch Checking

**Question:** Do all three methods give the same result?
- **Answer:** Yes! All show the current branch name

**Which is simplest?**
- **Answer:** `git branch --show-current` (most straightforward)

## ✅ Check Your Understanding - Answers

### Question 1: Command Differences

**Command A:** `git branch`
- Shows all local branches
- Current branch marked with * and green

**Command B:** `git branch -a`
- Shows all branches (local + remote)
- Remote branches shown as `remotes/origin/name`

**Command C:** `git branch -v`
- Shows all local branches with commit info
- Displays commit hash and message

### Question 2: Which branch are you on?

```
  develop
* main
  feature
```

**Answer:** `main`
- The asterisk marks the current branch

### Question 3: Check branch in one word

**Answer:** `git branch --show-current`

Or alternatives:
- `git rev-parse --abbrev-ref HEAD`
- `git symbolic-ref --short HEAD`

### Question 4: Does creating a branch switch to it?

**Answer:** NO!

- `git branch name` only creates
- `git checkout name` or `git switch name` switches to it
- `git checkout -b name` does both (create + switch)

### Question 5: Create AND switch command

**Answer:** `git checkout -b branch-name`

Or modern alternative:
- `git switch -c branch-name`

## 🎓 Challenge Exercises - Solutions

### Challenge 1: Branch Checking in a Script

**Output:** Should show: `You are currently on branch: <your-current-branch>`

This is useful for:
- CI/CD scripts
- Deployment automation
- Git workflows

### Challenge 2: Add Branch to Terminal Prompt

After configuration, your prompt might look like:
```
user@computer ~/project (main)$
```

**Benefits:**
- Always see current branch
- Prevents accidental commits to wrong branch
- No need to run `git branch` constantly

### Challenge 3: Find Current Branch Without Git

**Question:** Does this work?
- **Answer:** Yes! But only for attached HEAD

**Advantage of git commands:**
- Handle detached HEAD state
- More reliable across Git versions
- Clearer intent in code

### Challenge 4: Branches Containing a Commit

**Question:** Which branches contain the commit?
- **Answer:** Only `main` (and any branches created from it before new commits)
- Branches that diverged won't contain that specific commit

## 🔑 Key Takeaways

### 1. Multiple Ways to Check Current Branch

| Method | Shows | Use Case |
|--------|-------|----------|
| `git branch` | All branches, * on current | Quick visual check |
| `git status` | Current branch + file status | General status check |
| `git branch --show-current` | Current branch name only | Scripts, automation |
| `cat .git/HEAD` | HEAD reference | Understanding internals |

### 2. The Asterisk (*) Is Key

```
  develop
* main
  feature
```

- Asterisk = You are here
- Also typically shown in green
- Only one branch can be current at a time

### 3. Creating vs Switching

**Create only:**
```bash
git branch new-branch
# Creates but doesn't switch
```

**Switch only:**
```bash
git checkout existing-branch
# or: git switch existing-branch
```

**Create + Switch:**
```bash
git checkout -b new-branch
# or: git switch -c new-branch
```

### 4. Branch Listing Options

```bash
git branch              # Local branches
git branch -a           # All (local + remote)
git branch -r           # Remote only
git branch -v           # With commit info
git branch -vv          # With tracking info
git branch --merged     # Merged into current
git branch --no-merged  # Not yet merged
```

### 5. For Scripts and Automation

**Best options:**
```bash
# Modern, clear
git branch --show-current

# Alternative (works in older Git versions)
git rev-parse --abbrev-ref HEAD

# Manual but educational
cat .git/HEAD | sed 's/ref: refs\/heads\///'
```

## 📊 Visual Summary

### Branch Display in Terminal

```bash
$ git branch
  develop
  feature-login
* main
  staging

Key:
* = Current branch (also green)
  = Other branches
```

### What Each Command Shows

```
git branch
├── * main          ← You are here
├── develop
└── feature

git branch -v
├── * main    a1b2c3d Fix bug      ← Current + commit info
├── develop   c3d4e5f Add feature
└── feature   e5f6g7h Update docs

git branch -a
├── * main                          ← Local current
├── develop
├── feature
├── remotes/origin/main            ← Remote tracking
└── remotes/origin/develop
```

### Branch Lifecycle

```
Create Branch:
git branch feature → Creates, doesn't switch
Current: main

Switch Branch:
git checkout feature → Switches
Current: feature

Create + Switch:
git checkout -b bugfix → Creates & switches
Current: bugfix
```

## 🔧 Common Commands Reference

### Essential Commands

```bash
# Check current branch
git branch --show-current

# List all local branches
git branch

# List all branches (including remote)
git branch -a

# Show current branch status
git status

# Quick check for scripts
git rev-parse --abbrev-ref HEAD
```

### Advanced Commands

```bash
# Show branches with last commit
git branch -v

# Show branches with tracking info
git branch -vv

# Show merged branches
git branch --merged

# Show unmerged branches
git branch --no-merged

# Branches containing a commit
git branch --contains <commit>

# Branches not containing a commit
git branch --no-contains <commit>
```

## 🚀 Real-World Usage

### Before Making Changes
```bash
# Always check current branch first!
git branch --show-current

# If on wrong branch:
git switch correct-branch
```

### In Scripts
```bash
#!/bin/bash
CURRENT_BRANCH=$(git branch --show-current)

if [ "$CURRENT_BRANCH" != "main" ]; then
    echo "Error: Must be on main branch"
    exit 1
fi
```

### In CI/CD
```bash
# GitHub Actions example
if: github.ref == 'refs/heads/main'
```

### Terminal Prompt Setup
```bash
# Add to ~/.bashrc or ~/.zshrc
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
PS1='[\u@\h \W$(parse_git_branch)]$ '
```

## 💡 Pro Tips

1. **Always check before committing** - Wrong branch commits are common mistakes
2. **Use terminal prompts** - Show branch name permanently in prompt
3. **For scripts, use** `--show-current` - Cleaner than parsing `git branch`
4. **Learn the colors** - Green with * = current, white = others
5. **Remember** `checkout -b` - Fastest way to create and switch

## 🚀 What's Next?

Now that you know how to check your current branch, learn what happens when you stage files!

Continue to [Question 08: What Happens with git add .?](../question-08/)
