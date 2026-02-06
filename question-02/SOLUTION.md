# Solution: What is HEAD in Git?

## ✅ Answers to Exercise Questions

### Task 1: Understanding Default HEAD

**Question:** What does it say?
- **Answer:** `ref: refs/heads/master` (or `ref: refs/heads/main`)
- This is a symbolic reference pointing to the master/main branch
- It means HEAD is "attached" to the master branch

### Task 2: Create Commits and Watch HEAD Move

**Question:** What commit does HEAD point to?
- **Answer:** The first commit you created (you'll see something like `a1b2c3d Initial commit`)
- HEAD points to master, which points to this commit

**Question:** Did HEAD move to the new commit?
- **Answer:** Yes! HEAD (via master) now points to the newest commit
- This is automatic - when you commit, the current branch (and HEAD with it) moves forward

### Task 3: HEAD and Branches

**Question:** Which branch has the asterisk (*) next to it?
- **Answer:** `master` (or `main`)
- The asterisk shows which branch you're currently on

**Question:** Where is HEAD pointing?
- **Answer:** Still at master (or main)
- Creating a branch doesn't move HEAD, only switching does

**Question:** What does HEAD point to now? (after switching)
- **Answer:** `ref: refs/heads/feature-branch`
- HEAD now points to the feature-branch

### Task 4: Create Commits on Different Branches

**Question:** Do you see the "Add feature" commit on master? Why or why not?
- **Answer:** No, you don't see it
- **Why:** The "Add feature" commit was made on feature-branch, not master
- Each branch has its own commit history
- Commits on one branch don't automatically appear on others

**Question:** Where is HEAD pointing now?
- **Answer:** `ref: refs/heads/master`
- HEAD moved back to master when you switched branches

### Task 5: Experience Detached HEAD

**Question:** What does Git warn you about?
- **Answer:** Something like: "You are in 'detached HEAD' state"
- Git warns that you're not on any branch
- Any new commits you make might be lost if you switch away

**Question:** Does HEAD point to a branch or a commit?
- **Answer:** Directly to a commit (you'll see the commit hash, not a ref)
- Example: HEAD contains `a1b2c3d` instead of `ref: refs/heads/master`

### Task 6: Visualize HEAD with Git Log

**Question:** Can you see where HEAD points in this visualization?
- **Answer:** Yes! You'll see `HEAD ->` in the output
- Example: `* a1b2c3d (HEAD -> master) Second commit`
- This shows HEAD is attached to master, which is at that commit

## ✅ Check Your Understanding - Answers

### 1. What happens to HEAD when you create a new commit?

**Answer:** HEAD (and the branch it points to) automatically moves forward to the new commit.

**Visual:**
```
Before commit:
HEAD → master → commit A

After commit:
HEAD → master → commit B
                   ↑
               commit A
```

### 2. What's the difference between these two?

**Scenario 1:** `HEAD → master → commit123`
- **Answer:** HEAD is attached to a branch (master)
- Normal, safe state
- When you commit, master moves forward and takes HEAD with it

**Scenario 2:** `HEAD → commit123`
- **Answer:** HEAD is detached (not pointing to any branch)
- You're viewing a specific commit directly
- If you commit here, the commit isn't on any branch and could be lost

### 3. Why is "detached HEAD" called "detached"?

**Answer:** Because HEAD is detached (disconnected) from any branch name.

- **Normal:** HEAD → branch → commit (attached)
- **Detached:** HEAD → commit (no branch involved)

It's "detached" from the branch system. Any commits you make won't be associated with a branch, making them easy to lose.

### 4. If you make a commit while in detached HEAD state, what happens?

**Answer:** The commit is created but isn't on any branch.

**Risk:** If you switch to another branch without saving it, the commit becomes "orphaned" and might be garbage-collected by Git later.

**Solution:** Create a new branch from detached HEAD:
```bash
git checkout -b new-branch-name
```

## 🎓 Challenge Exercises - Solutions

### Challenge 1: HEAD Movement - Sample Output

After completing the steps, your graph might look like:

```
* e4f5g6h (dev, HEAD) Commit 5
* c3d4e5f Commit 4
| * 9a0b1c2 (master) Commit 3
| * 7889a0b Commit 2
|/
* a1b2c3d Commit 1
```

This shows:
- HEAD is on `dev` branch
- `dev` has 5 commits
- `master` has 3 commits
- They diverged after Commit 1

### Challenge 2: Safe Detached HEAD - Explanation

```bash
# Start detached
git checkout a1b2c3d
# HEAD → a1b2c3d (detached)

# Create branch from here
git checkout -b experiment
# HEAD → experiment → a1b2c3d (attached!)

# Now safe to commit
echo "test" > test.txt
git add test.txt
git commit -m "Experiment commit"
# HEAD → experiment → new_commit (still attached)
```

**Key insight:** Creating a branch from detached HEAD "re-attaches" HEAD to that new branch.

### Challenge 3: HEAD Reference - Explanations

```bash
git show HEAD
# Shows the commit HEAD points to (latest commit)

git show HEAD~1
# Shows the parent of HEAD (one commit back)
# ~ means "parent"

git show HEAD~2
# Shows the grandparent of HEAD (two commits back)

git diff HEAD~1 HEAD
# Shows what changed between last commit and current commit
```

**HEAD~N notation:**
- `HEAD~1` or `HEAD~` = parent commit
- `HEAD~2` = grandparent commit
- `HEAD~3` = great-grandparent commit

## 🔑 Key Takeaways

### 1. What is HEAD?
HEAD is a pointer to your current position in the Git repository.

### 2. Normal State (Attached HEAD)
```
HEAD → branch → commit
```
- HEAD points to a branch
- Branch points to a commit
- Commits update the branch automatically

### 3. Detached HEAD State
```
HEAD → commit
```
- HEAD points directly to a commit
- No branch involved
- Risky: new commits can be lost

### 4. HEAD Movement

| Action | HEAD Moves To |
|--------|---------------|
| `git commit` | New commit (via current branch) |
| `git checkout branch` | That branch |
| `git checkout commit-hash` | That commit (detached) |
| `git switch branch` | That branch |

### 5. Useful HEAD Commands

```bash
cat .git/HEAD                    # See what HEAD points to
git log --oneline --graph        # Visualize HEAD position
git show HEAD                    # Show current commit
git diff HEAD~1 HEAD             # See recent changes
git checkout -b new-branch       # Create branch from current HEAD
```

## 📊 Visual Summary

### Attached HEAD (Normal)
```
           HEAD
            ↓
          master
            ↓
         commit C
            ↓
         commit B
            ↓
         commit A
```

### Detached HEAD (Risky)
```
           HEAD
            ↓
         commit B
            ↓
         commit A
        
      (No branch!)
```

### Multiple Branches
```
    HEAD
     ↓
  feature-branch
     ↓
  commit D
     ↓
  commit C ←── master
     ↓
  commit B
     ↓
  commit A
```

## 🚀 What's Next?

Now that you understand HEAD, you're ready to learn about tracked and untracked files!

Continue to [Question 03: Tracked vs Untracked Files](../question-03/)
