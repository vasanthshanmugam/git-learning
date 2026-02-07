# Question 12: What is git cherry-pick and When Would You Use It?

## 📝 Question
What is git cherry-pick and when would you use it?

## 🎯 Learning Objectives
By completing this exercise, you will understand:
- What cherry-pick does
- When to use cherry-pick
- How to cherry-pick on GitHub
- The difference between cherry-pick and merge
- Common use cases in real projects
- How to validate cherry-picked commits

## 🔍 Concept Overview

### What is Cherry-Pick?

**Cherry-pick** = Copy a specific commit from one branch to another

Think of it like:
- "I want ONLY this commit, not the whole branch"
- Selective commit copying
- Applying specific changes without merging everything

### Visual Example

```
feature branch:  A -- B -- C -- D -- E
                      ↑
                 (want only commit C)
                      
main branch:     X -- Y -- C' 
                           ↑
                    (cherry-picked copy of C)
```

### When to Use Cherry-Pick

**Good use cases:**
1. **Hotfix:** Bug fix on feature branch, need it on main NOW
2. **Selective feature:** Want one commit, not entire branch
3. **Backport:** Apply fix to older version
4. **Mistake recovery:** Commit went to wrong branch

**Avoid when:**
- You want entire branch → use merge instead
- Many commits needed → consider merging
- Causes conflicts → might be simpler to merge

## 💻 GitHub-Based Exercise

### Prerequisites

- Forked `git-learning-practice-repo`
- Completed Questions 10-11

### Task 1: Understanding the Setup

**On GitHub:**

1. Go to your forked repo
2. Switch to `feature-b` branch
3. View commit history

**Question:** How many commits does feature-b have that main doesn't? _________________

**List the commit messages:**
1. _________________
2. _________________

**Scenario:** You want ONLY the "Update changelog" commit on main, not the "Add divide function" commit.

### Task 2: Find the Commit to Cherry-Pick

**On GitHub - feature-b branch:**

1. Click on "commits" (next to branch name)
2. Find "Update changelog for divide function" commit
3. Click on that commit
4. Look at the URL - it contains the commit hash

**Question:** What's the commit hash? (copy first 7 characters) _________________

**Question:** What file does this commit change? _________________

### Task 3: Cherry-Pick Using GitHub Web Interface

**Method 1: Using GitHub's Interface (if available)**

Note: GitHub doesn't have a direct cherry-pick button, so we'll do this via your computer, but validate on GitHub.

**On Your Computer:**

```bash
cd ~/Desktop/git-learning-practice-repo
git pull origin main
git checkout main
```

Get the commit hash from Task 2, then:

```bash
git cherry-pick <commit-hash>
# Example: git cherry-pick 5ed1eac
```

**Question:** Did it work? _________________

**Question:** Any conflicts? _________________

Push to GitHub:

```bash
git push origin main
```

**Validation on GitHub:**

1. Go to main branch
2. View commit history
3. Find the cherry-picked commit

**Questions:**
- Do you see "Update changelog for divide function"? _________________
- Is the commit hash DIFFERENT from the original? _________________
- Can you see the original commit on feature-b still? _________________

### Task 4: Understand What Got Cherry-Picked

**On GitHub - main branch:**

1. Click on the cherry-picked commit
2. View the changes

**Questions:**
- What file was modified? _________________
- Did it bring the "divide function" code? _________________
- Did it bring ONLY the changelog update? _________________

**Understanding:** Cherry-pick copied ONLY that specific commit's changes!

### Task 5: Compare Original vs Cherry-Picked Commit

**On GitHub:**

**View original commit on feature-b:**
1. Switch to feature-b branch
2. Find "Update changelog" commit
3. Note the commit hash

**View cherry-picked commit on main:**
1. Switch to main branch
2. Find "Update changelog" commit
3. Note the commit hash

**Question:** Are the hashes identical? _________________

**Question:** Are the CHANGES identical? _________________

**Understanding:** Cherry-pick creates a NEW commit with the SAME changes!

### Task 6: Visualize in Network Graph

**On GitHub:**

1. Go to Insights → Network
2. Look at the graph

**Questions:**
- Can you see where feature-b commits are? _________________
- Can you see the cherry-picked commit on main? _________________
- Does it show a connection between them? _________________

**Note:** Cherry-pick doesn't show as a merge - it's a separate commit!

### Task 7: Cherry-Pick Multiple Commits

**Scenario:** Now let's cherry-pick the divide function commit too

**On Your Computer:**

Find the "Add divide function" commit hash from feature-b:

```bash
git log origin/feature-b --oneline
# Find the commit hash for "Add divide function"

git checkout main
git cherry-pick <commit-hash-of-divide-function>
git push origin main
```

**Validation on GitHub - main branch:**

1. Check `app.js`
2. Look for divide function

**Questions:**
- Is the divide function now on main? _________________
- Did you merge the entire feature-b branch? _________________
- How many commits did you cherry-pick total? _________________

### Task 8: Cherry-Pick vs Merge Comparison

**On GitHub - Create a comparison:**

**Current state:**
- main has: 2 cherry-picked commits from feature-b
- feature-b still exists with its original commits

**Question:** If you now merge feature-b into main, what will happen?
- A) Nothing (already up to date)
- B) Duplicate commits
- C) Conflicts
- D) New merge commit

**Try it (optional):**

```bash
git checkout main
git merge origin/feature-b
```

**Question:** What happened? _________________

### Task 9: Real-World Scenario - Hotfix

**Practice realistic cherry-pick workflow:**

**On GitHub:**

1. Create new branch from `feature-a` called `experiment`
2. On `experiment`, make a small change (edit README)
3. Commit: "Fix typo in README"
4. You realize this fix is needed on `main` immediately!

**On Your Computer:**

```bash
git fetch origin
git log origin/experiment --oneline -3
# Find the "Fix typo" commit hash

git checkout main
git cherry-pick <fix-typo-commit-hash>
git push origin main
```

**Validation on GitHub:**

**Questions:**
- Is the typo fix on main? _________________
- Is it also still on experiment? _________________
- Did you have to merge all of experiment? _________________

**Understanding:** This is how hotfixes work - fix on feature branch, cherry-pick to main!

### Task 10: Identify When NOT to Cherry-Pick

**On GitHub:**

Look at `feature-a` branch:
- Has "Add subtract function" commit

**Question:** Should you cherry-pick this to main, or merge the branch?

Consider:
- How many commits need to go to main? _________________
- Are the commits related? _________________
- Is feature-a ready to merge completely? _________________

**Best practice:** If you need most/all commits from a branch, MERGE don't cherry-pick!

## ✅ Check Your Understanding

### Question 1: What does cherry-pick do?

**Answer:** _________________

### Question 2: When should you use cherry-pick instead of merge?

**Answer:** _________________

### Question 3: True or False

"Cherry-picking creates a new commit with a new hash."

**Answer:** _________________

### Question 4: If you cherry-pick a commit, does it disappear from the original branch?

**Answer:** _________________

### Question 5: Complete the analogy

"Merge is like _________________, while cherry-pick is like _________________."

**Answer:** _________________

## 🎓 Challenge Exercises

### Challenge 1: Cherry-Pick with Conflict

**Create a conflict:**

1. On main, edit app.js line 10
2. Commit: "Update line 10 on main"
3. Try cherry-picking a commit from feature-b that also changes line 10

**Question:** What happens? _________________

**Resolve it:**
- Fix the conflict
- Continue cherry-pick
- Validate on GitHub

### Challenge 2: Cherry-Pick Range

**On Your Computer:**

```bash
# Cherry-pick multiple commits at once
git cherry-pick <commit-hash-1> <commit-hash-2> <commit-hash-3>

# Or use range
git cherry-pick <start-hash>..<end-hash>
```

**Question:** How is this different from merge? _________________

### Challenge 3: Undo a Cherry-Pick

**If you cherry-picked by mistake:**

```bash
git cherry-pick <hash>
# Oops! Wrong commit!

# Before pushing, undo:
git reset --hard HEAD~1
```

**Question:** Is the commit gone? _________________

## 📚 Solution

Ready to check your work? See [SOLUTION.md](./SOLUTION.md)

## 🔗 Congratulations!

You've completed Questions 10-12! You now understand:
- ✅ git clone vs git pull
- ✅ Fast-forward vs three-way merge
- ✅ git cherry-pick

### Your Complete Progress
All 12 questions completed! 🎉

---

## 💡 Quick Reference

### Cherry-Pick a Commit
```bash
# Find the commit hash
git log branch-name --oneline

# Cherry-pick it
git cherry-pick <commit-hash>

# Push to GitHub
git push origin current-branch
```

### Cherry-Pick Multiple
```bash
# Specific commits
git cherry-pick hash1 hash2 hash3

# Range
git cherry-pick start-hash..end-hash
```

### Handle Conflicts
```bash
git cherry-pick <hash>
# If conflict occurs:
# 1. Fix conflicts in files
git add .
git cherry-pick --continue

# Or abort
git cherry-pick --abort
```

## 🎯 Key Takeaways

**Cherry-Pick:**
- ✅ Copies specific commits
- ✅ Creates new commit (different hash)
- ✅ Original commit stays on source branch
- ✅ Use for selective changes
- ✅ Don't overuse - merge is often better

**Use Cases:**
- Hotfixes
- Bug fixes to backport
- Specific feature from branch
- Wrong branch commits

**Validate on GitHub:**
- Check commit history
- View file changes
- Compare hashes
- Use network graph
