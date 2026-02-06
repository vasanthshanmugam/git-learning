# Question 03: Tracked vs Untracked Files

## 📝 Question
What is the difference between tracked and untracked files?

## 🎯 Learning Objectives
By completing this exercise, you will understand:
- What makes a file "tracked" or "untracked"
- How Git starts tracking files
- The lifecycle of a file in Git
- How to stop tracking files (but keep them in your project)

## 🔍 Concept Overview

### Tracked Files
**Tracked files** are files that Git knows about and monitors for changes.

Characteristics:
- Git has recorded them in at least one commit
- Git watches for modifications to these files
- They appear in `git status` when modified
- Included in your repository's history

### Untracked Files
**Untracked files** exist in your working directory but Git ignores them.

Characteristics:
- Never been added to Git (never staged or committed)
- Git doesn't monitor them for changes
- Appear in `git status` as "Untracked files"
- Not included in commits unless you explicitly add them

### File States Lifecycle
```
Untracked → (git add) → Staged → (git commit) → Tracked
                                                   ↓
                                              Modified
                                                   ↓
                                           (git add) → Staged
```

## 💻 Hands-On Exercise

### Setup
Navigate to question-03 folder and initialize:

```bash
cd question-03
git init
```

### Task 1: Identify Untracked Files

Create several files:
```bash
echo "Main code" > app.js
echo "Test code" > test.js
echo "Documentation" > README.md
echo "Secret keys" > config.env
```

Check status:
```bash
git status
```

**Question:** How many untracked files do you see? _________________

**Question:** What color are they displayed in? _________________

### Task 2: Make Files Tracked

Add and commit one file:
```bash
git add app.js
git commit -m "Add main application"
```

Check status again:
```bash
git status
```

**Question:** Is app.js still listed? _________________

**Question:** Are the other files still untracked? _________________

**Key Point:** app.js is now **tracked** because Git has committed it.

### Task 3: Understand Tracked File Modifications

Modify the tracked file:
```bash
echo "Updated code" >> app.js
git status
```

**Question:** What section does app.js appear in now? _________________

**Question:** Is app.js tracked or untracked? _________________

**Important:** A tracked file can be in different states:
- **Unmodified** (tracked, no changes since last commit)
- **Modified** (tracked, but changed since last commit)
- **Staged** (tracked, changes ready for commit)

### Task 4: Track More Files

Add the remaining files:
```bash
git add test.js README.md
git commit -m "Add tests and documentation"
git status
```

**Question:** How many untracked files remain? _________________

**Question:** Which file is still untracked? _________________

### Task 5: Understanding .gitignore

You probably don't want to track `config.env` (it contains secrets).

Create a `.gitignore` file:
```bash
echo "config.env" > .gitignore
git status
```

**Question:** Does config.env appear as untracked anymore? _________________

**Question:** What new file appears? _________________

Add and commit .gitignore:
```bash
git add .gitignore
git commit -m "Add gitignore"
git status
```

**Question:** Do you see config.env now? _________________

### Task 6: Untrack a File (But Keep It)

Sometimes you accidentally track a file you shouldn't have.

Let's say you tracked config.env by mistake:
```bash
# First, let's track it (this is the mistake)
git add config.env
git commit -m "Accidentally added config"
git status
```

Now config.env is tracked. But you want to untrack it without deleting it:

```bash
git rm --cached config.env
git status
```

**Question:** What status does config.env have now? _________________

**Question:** Does the file still exist in your folder? _________________

Add it to .gitignore:
```bash
echo "config.env" >> .gitignore
git add .gitignore
git commit -m "Stop tracking config.env"
```

### Task 7: Complete File Lifecycle

Create a new file and move it through all states:

```bash
# 1. Create file (Untracked)
echo "New feature" > feature.js
git status

# 2. Stage it (Tracked, staged)
git add feature.js
git status

# 3. Modify it before committing (Tracked, staged AND modified)
echo "More features" >> feature.js
git status
```

**Question:** Can you see feature.js in TWO sections? _________________

**Question:** Why is it in both places? _________________

Commit both versions:
```bash
git add feature.js
git commit -m "Add feature"
git status
```

## ✅ Check Your Understanding

1. **Can a file be both tracked and untracked at the same time?**
   - Answer: _________________

2. **If you delete a tracked file from your working directory, is it still tracked?**
   - Answer: _________________

3. **What's the difference between `git rm file.txt` and `git rm --cached file.txt`?**
   - Answer: _________________

4. **Once a file is committed, is it permanently tracked forever?**
   - Answer: _________________

5. **What happens if you modify a tracked file but don't stage it before committing?**
   - Answer: _________________

## 🎓 Challenge Exercises

### Challenge 1: Track Patterns
1. Create files: `notes1.txt`, `notes2.txt`, `notes3.txt`
2. Add all of them at once using: `git add *.txt`
3. Check which ones are tracked

### Challenge 2: Mixed States
1. Create and commit `data.json`
2. Modify it
3. Stage the changes
4. Modify it again (without staging)
5. Run `git status` - explain what you see

### Challenge 3: Gitignore Patterns
Create a .gitignore that ignores:
- All `.log` files
- A folder called `temp/`
- All files in `build/` but not the folder itself
- A specific file `secrets.txt`

Then create some of these files and verify they're ignored.

### Challenge 4: Tracking Status
Run these commands and explain what each shows:
```bash
git ls-files                    # What does this list?
git status --short              # What's the difference from normal status?
git status --untracked-files=no # What disappeared?
```

## 📚 Solution

Ready to check your work? See [SOLUTION.md](./SOLUTION.md)

## 🔗 What's Next?

Congratulations! You've completed the first 3 fundamental Git questions. 

**Your Progress:**
- ✅ Question 01: Working Directory, Staging Area, and Repository
- ✅ Question 02: What is HEAD in Git?
- ✅ Question 03: Tracked vs Untracked Files

**Keep practicing!** The best way to learn Git is by using it. Try these exercises multiple times until the concepts feel natural.

More questions coming soon! Star this repository to get notified when new content is added.
