# Question 02: What is HEAD in Git?

## 📝 Question
What is a HEAD in Git?

## 🎯 Learning Objectives
By completing this exercise, you will understand:
- What HEAD is and why it's important
- How HEAD points to your current location in Git
- How HEAD changes when you switch branches or commits
- The concept of "detached HEAD"

## 🔍 Concept Overview

### What is HEAD?

**HEAD** is a pointer that tells Git where you currently are in your repository's history.

Think of HEAD as a "You Are Here" marker on a map:
- It points to the current branch you're on
- Which points to the latest commit on that branch
- This tells Git which snapshot of your project you're looking at

### Visual Representation
```
HEAD → master → commit abc123
```

This means:
- You're on the `master` branch
- `master` points to commit `abc123`
- Your working directory shows files from commit `abc123`

### Key Points
1. **HEAD is usually attached to a branch name** (like `main` or `master`)
2. **When you make a commit**, HEAD (and the branch) moves forward
3. **When you switch branches**, HEAD moves to point to the new branch
4. **Detached HEAD** happens when HEAD points directly to a commit, not a branch

## 💻 Hands-On Exercise

### Setup
Navigate to the question-02 folder and initialize:

```bash
cd question-02
git init
```

### Task 1: Understanding Default HEAD

Check where HEAD is pointing:

```bash
cat .git/HEAD
```

**Question:** What does it say? _________________

It probably says: `ref: refs/heads/master` (or `main`)

This means HEAD points to the master branch.

### Task 2: Create Commits and Watch HEAD Move

Create first commit:
```bash
echo "First version" > project.txt
git add project.txt
git commit -m "Initial commit"
```

Check commit history:
```bash
git log --oneline
```

**Question:** What commit does HEAD point to? _________________

Create second commit:
```bash
echo "Second version" >> project.txt
git add project.txt
git commit -m "Add second version"
```

Check history again:
```bash
git log --oneline
```

**Question:** Did HEAD move to the new commit? _________________

### Task 3: HEAD and Branches

Create a new branch:
```bash
git branch feature-branch
git branch
```

**Question:** Which branch has the asterisk (*) next to it? _________________

**Question:** Where is HEAD pointing? _________________

Check HEAD:
```bash
cat .git/HEAD
```

Now switch to the new branch:
```bash
git checkout feature-branch
# or: git switch feature-branch
cat .git/HEAD
```

**Question:** What does HEAD point to now? _________________

### Task 4: Create Commits on Different Branches

On feature-branch, create a commit:
```bash
echo "Feature work" > feature.txt
git add feature.txt
git commit -m "Add feature"
git log --oneline
```

Switch back to master:
```bash
git checkout master
# or: git switch master
git log --oneline
```

**Question:** Do you see the "Add feature" commit on master? Why or why not?
- Answer: _________________

**Question:** Where is HEAD pointing now? _________________

### Task 5: Experience Detached HEAD

View your commit history:
```bash
git log --oneline
```

Pick the first commit hash and checkout to it directly:
```bash
git checkout <first-commit-hash>
# Example: git checkout a1b2c3d
```

Read the warning message!

**Question:** What does Git warn you about? _________________

Check HEAD:
```bash
cat .git/HEAD
```

**Question:** Does HEAD point to a branch or a commit? _________________

Return to master branch:
```bash
git checkout master
# or: git switch master
```

### Task 6: Visualize HEAD with Git Log

```bash
git log --oneline --all --graph --decorate
```

This shows:
- All branches
- Where HEAD is pointing
- Commit relationships

**Question:** Can you see where HEAD points in this visualization? _________________

## ✅ Check Your Understanding

1. **What happens to HEAD when you create a new commit?**
   - Answer: _________________

2. **What's the difference between these two?**
   - `HEAD → master → commit123`
   - `HEAD → commit123`
   - Answer: _________________

3. **Why is "detached HEAD" called "detached"?**
   - Answer: _________________

4. **If you make a commit while in detached HEAD state, what happens?**
   - Answer: _________________

## 🎓 Challenge Exercises

### Challenge 1: HEAD Movement
1. Create 3 commits on master
2. Create a new branch `dev`
3. Switch to `dev` and create 2 commits
4. Switch back to master
5. Use `git log --oneline --all --graph` to visualize where HEAD is

### Challenge 2: Safe Detached HEAD
1. Checkout to an old commit (detached HEAD)
2. Create a new branch from there: `git checkout -b experiment`
3. Now you're no longer detached! Make a commit to prove it.

### Challenge 3: HEAD Reference
Try these commands and observe output:
```bash
git show HEAD           # Show latest commit
git show HEAD~1         # Show commit before HEAD
git show HEAD~2         # Show commit 2 before HEAD
git diff HEAD~1 HEAD    # Difference between last and current commit
```

## 📚 Solution

Ready to check your work? See [SOLUTION.md](./SOLUTION.md)

## 🔗 Next Steps
Once you've mastered HEAD, move to [Question 03: Tracked vs Untracked Files](../question-03/)
