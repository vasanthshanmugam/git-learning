# Question 07: How Do You Check the Current Branch?

## 📝 Question
How do you check the current branch?

## 🎯 Learning Objectives
By completing this exercise, you will understand:
- Multiple ways to check your current branch
- How to see all branches (local and remote)
- What the asterisk (*) means in branch listings
- Where Git stores current branch information
- Quick ways to show branch in terminal

## 🔍 Concept Overview

### Why Check the Current Branch?

Knowing your current branch is critical because:
- Different branches have different code versions
- Commits go to the current branch only
- You might be on the wrong branch by mistake
- Prevents accidental commits to main/production

### Multiple Ways to Check

Git provides several methods:
1. `git branch` - List branches, shows current with *
2. `git status` - Shows current branch in output
3. `git branch --show-current` - Shows only current branch name
4. Check `.git/HEAD` file directly
5. Terminal prompt (if configured)

## 💻 Hands-On Exercise

### Setup: Create a Practice Repository

```bash
cd ~/Desktop
mkdir branch-check-practice
cd branch-check-practice
git init
```

### Task 1: Check Branch Before First Commit

Try to check the current branch:

```bash
git branch
```

**Question:** What do you see? _________________

**Why is the list empty?** _________________

Now try:

```bash
git status
```

**Question:** What does it say about the branch? _________________

### Task 2: Create First Commit and Check Again

```bash
echo "Initial file" > readme.txt
git add readme.txt
git commit -m "Initial commit"
```

Now check branches:

```bash
git branch
```

**Question:** What branch appears? _________________

**Question:** Is there an asterisk (*) next to it? _________________

**What does the asterisk mean?** _________________

### Task 3: Multiple Ways to Check Current Branch

Try all these methods:

#### Method 1: git branch
```bash
git branch
```

**Output:** _________________

#### Method 2: git status
```bash
git status
```

**Question:** Which line tells you the branch? _________________

#### Method 3: git branch --show-current
```bash
git branch --show-current
```

**Question:** What does this show? _________________

**Question:** How is this different from `git branch`? _________________

#### Method 4: Check HEAD file
```bash
cat .git/HEAD
```

**Question:** What does it say? _________________

**Question:** Can you see the branch name in there? _________________

### Task 4: Create Multiple Branches and Practice

Create some branches:

```bash
git branch feature
git branch bugfix
git branch experimental
```

List all branches:

```bash
git branch
```

**Question:** How many branches do you see? _________________

**Question:** Which one has the asterisk? _________________

**Question:** What does this tell you? _________________

### Task 5: Switch Branches and Check

Switch to a different branch:

```bash
git checkout feature
# or: git switch feature
```

Check current branch:

```bash
git branch
```

**Question:** Which branch has the asterisk now? _________________

Quick check:

```bash
git branch --show-current
```

**Output:** _________________

Switch to another branch:

```bash
git switch bugfix
git branch --show-current
```

**Output:** _________________

### Task 6: See All Branches Including Remote

First, let's simulate having remote branches:

```bash
# Go back to main branch
git switch master  # or main

# Create more branches
git branch dev
git branch staging
```

List local branches only:

```bash
git branch
```

**Question:** How many branches are listed? _________________

List all branches (including remote tracking):

```bash
git branch -a
```

**Question:** Do you see any remote branches? _________________

**Note:** You won't see remotes yet because we haven't set up a remote. This command is useful when you've cloned from GitHub.

### Task 7: Verbose Branch Information

Get detailed branch info:

```bash
git branch -v
```

**Question:** What extra information does this show? _________________

**Question:** Does it show commit hashes? _________________

### Task 8: Current Branch in Different Scenarios

#### Scenario A: After creating a new branch
```bash
git branch new-feature
git branch --show-current
```

**Question:** Are you on new-feature? _________________

**Why/why not?** _________________

#### Scenario B: After switching branches
```bash
git checkout new-feature
git branch --show-current
```

**Question:** Now are you on new-feature? _________________

#### Scenario C: After creating AND switching
```bash
git checkout -b quick-feature
git branch --show-current
```

**Question:** What branch are you on? _________________

**What did `git checkout -b` do?** _________________

### Task 9: Understanding Branch Output Colors

Look at the branch list:

```bash
git branch
```

**Question:** What color is the current branch? _________________

**Question:** What color are other branches? _________________

**Color meanings:**
- Green (with asterisk) = Current branch
- White/default = Other branches

### Task 10: Programmatic Branch Checking

These are useful for scripts:

```bash
# Method 1: Show current branch name only
git branch --show-current

# Method 2: Using rev-parse
git rev-parse --abbrev-ref HEAD

# Method 3: Using symbolic-ref
git symbolic-ref --short HEAD
```

**Question:** Do all three methods give the same result? _________________

**Which is simplest?** _________________

## ✅ Check Your Understanding

### Question 1: What's the difference between these commands?

```bash
git branch              # Command A
git branch -a           # Command B
git branch -v           # Command C
```

**Answers:**
- Command A: _________________
- Command B: _________________
- Command C: _________________

### Question 2: If you see this output, which branch are you on?

```
  develop
* main
  feature
```

**Answer:** _________________

### Question 3: How can you check your branch in one word (just the name)?

**Answer:** _________________

### Question 4: Does creating a branch automatically switch to it?

Test it:
```bash
git branch test-branch
git branch --show-current
```

**Answer:** _________________

### Question 5: What command both creates AND switches to a new branch?

**Answer:** _________________

## 🎓 Challenge Exercises

### Challenge 1: Branch Checking in a Script

Create a simple shell script that shows your current branch:

```bash
#!/bin/bash
echo "You are currently on branch: $(git branch --show-current)"
```

Save it as `show-branch.sh`, make it executable, and run it:

```bash
echo '#!/bin/bash' > show-branch.sh
echo 'echo "You are currently on branch: $(git branch --show-current)"' >> show-branch.sh
chmod +x show-branch.sh
./show-branch.sh
```

**Output:** _________________

### Challenge 2: Add Branch to Terminal Prompt

This is optional but very useful! You can configure your terminal to always show the current branch.

For bash, add this to `~/.bashrc`:

```bash
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
PS1="\u@\h \w \$(parse_git_branch)$ "
```

**Try it:**
```bash
source ~/.bashrc
# Your prompt should now show the branch!
```

### Challenge 3: Find Current Branch Without Git Commands

```bash
# Read HEAD directly and extract branch name
cat .git/HEAD | sed 's/ref: refs\/heads\///'
```

**Question:** Does this work? _________________

**Question:** What's the advantage of using git commands instead? _________________

### Challenge 4: List Branches That Contain a Specific Commit

```bash
# Make several commits on different branches
git checkout main
echo "main work" > main.txt
git add main.txt
git commit -m "Main work"

git checkout feature
echo "feature work" > feature.txt
git add feature.txt
git commit -m "Feature work"

# Get a commit hash from main
git checkout main
git log --oneline | head -1

# See which branches contain this commit
git branch --contains <commit-hash>
```

**Question:** Which branches contain the commit? _________________

## 📚 Solution

Ready to check your work? See [SOLUTION.md](./SOLUTION.md)

## 🔗 Next Steps
Once you've mastered checking branches, move to [Question 08: What Happens with git add .?](../question-08/)

---

## 💡 Quick Reference

### Check Current Branch
```bash
git branch                      # List all, current marked with *
git branch --show-current       # Show current name only
git status                      # Shows branch in output
cat .git/HEAD                   # Direct file check
```

### List Branches
```bash
git branch                      # Local branches only
git branch -a                   # All (local + remote)
git branch -r                   # Remote branches only
git branch -v                   # With last commit info
git branch -vv                  # With tracking info
```

### Quick Shortcuts
```bash
# Current branch name for scripts
git branch --show-current

# Alternative (older method)
git rev-parse --abbrev-ref HEAD
```
