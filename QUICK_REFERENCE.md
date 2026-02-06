# Git Quick Reference - Questions 1-3

This is a quick reference for the concepts covered in the first 3 questions.

## Question 01: Three Areas in Git

```
Working Directory  →  Staging Area  →  Repository
     (modify)         (git add)        (git commit)
```

| Area | What It Is | Commands |
|------|------------|----------|
| **Working Directory** | Your project folder | Edit files normally |
| **Staging Area** | Preparation for commit | `git add <file>` |
| **Repository** | Permanent Git history | `git commit -m "msg"` |

### Common Commands
```bash
git status              # See which area files are in
git add file.txt        # Move to staging area
git commit -m "msg"     # Move to repository
git diff                # Working vs Staging
git diff --staged       # Staging vs Repository
```

## Question 02: HEAD

**HEAD** = Pointer to your current location in Git

### Normal (Attached HEAD)
```
HEAD → branch → commit
```

### Detached HEAD (Risky!)
```
HEAD → commit (no branch!)
```

### Common Commands
```bash
cat .git/HEAD                 # See what HEAD points to
git log --oneline --graph     # Visualize HEAD position
git show HEAD                 # Show current commit
git show HEAD~1               # Show previous commit
git checkout <branch>         # Move HEAD to branch
git checkout <commit-hash>    # Detached HEAD!
```

### HEAD Movement
- `git commit` → HEAD moves forward
- `git checkout branch` → HEAD points to that branch
- `git checkout commit` → HEAD detaches

## Question 03: Tracked vs Untracked

### File States
```
UNTRACKED → (git add) → TRACKED (staged) → (git commit) → TRACKED (committed)
                                                                   ↓
                                                            TRACKED (modified)
```

### Quick Check
| Status | Meaning | What To Do |
|--------|---------|------------|
| Red "Untracked files" | New file, Git doesn't know it | `git add <file>` |
| Red "Changes not staged" | Tracked file modified | `git add <file>` |
| Green "Changes to be committed" | Staged, ready to commit | `git commit -m "msg"` |
| Nothing to commit | All tracked files are committed | Keep working! |

### Common Commands
```bash
git status                   # See tracked/untracked files
git add file.txt            # Start tracking
git rm --cached file.txt    # Stop tracking (keep file)
git rm file.txt             # Stop tracking (delete file)
git ls-files                # List all tracked files
```

### .gitignore
```bash
# Create .gitignore
echo "*.log" > .gitignore    # Ignore all .log files
echo "temp/" >> .gitignore   # Ignore temp folder

# Common patterns
*.log           # All .log files
temp/           # temp directory
secrets.txt     # Specific file
build/*         # Everything in build/
!build/.keep    # Except this file
```

## Putting It All Together

### Complete Workflow
```bash
# 1. Create/modify files (Working Directory)
echo "Hello" > app.js

# 2. Check status
git status                    # app.js is untracked

# 3. Stage files (Staging Area)
git add app.js
git status                    # app.js is staged (green)

# 4. Commit (Repository)
git commit -m "Add app.js"
git status                    # Working tree clean

# 5. Modify tracked file
echo "World" >> app.js
git status                    # app.js is modified (red)

# 6. Stage and commit again
git add app.js
git commit -m "Update app.js"
```

### Common Scenarios

**Scenario: Made changes to 3 files, want to commit only 2**
```bash
git add file1.txt file2.txt    # Only stage these
git commit -m "Update 2 files" # Only commits staged files
# file3.txt remains modified but uncommitted
```

**Scenario: Accidentally tracked a secrets file**
```bash
git rm --cached secrets.txt    # Stop tracking
echo "secrets.txt" >> .gitignore  # Prevent future tracking
git add .gitignore
git commit -m "Stop tracking secrets"
```

**Scenario: Want to see where I am**
```bash
git log --oneline --graph --all
# Shows branches, HEAD position, and commit history
```

**Scenario: Exploring old commits**
```bash
git log --oneline              # Find commit hash
git checkout abc123d           # Go to that commit (detached HEAD!)
# Look around, test things
git checkout main              # Return to branch (attached HEAD)
```

## Color Meanings in `git status`

- 🟢 **Green** = Staged (ready for commit)
- 🔴 **Red** = Modified or untracked (needs attention)
- **No color** = Everything committed (clean working tree)

## Remember

1. **Three areas** = Working Directory → Staging Area → Repository
2. **HEAD** = Where you are right now
3. **Tracked** = Git knows about it
4. **Untracked** = Git ignores it (until you `git add`)

---

**Print this page and keep it handy while practicing!**
