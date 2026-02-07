# Git Quick Reference - Questions 1-6

This is a quick reference for the concepts covered in the first 6 questions.

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
5. **git init** = Creates `.git` folder (the repository)
6. **Default branch** = First branch created (master or main)
7. **.git directory** = IS the repository (all your data)

---

## Question 04: What Does git init Do?

### What It Creates
```bash
git init
# Creates:
.git/
├── HEAD              # Points to current branch
├── config            # Repository settings
├── objects/          # Database (empty initially)
├── refs/             # References (branches, tags)
└── hooks/            # Automation scripts
```

### Key Commands
```bash
git init                    # Initialize in current folder
git init myproject          # Create folder + initialize
ls -la .git                 # Explore .git structure
cat .git/HEAD               # See what HEAD points to
```

### Important Points
- `.git` appears after `git init`
- No branches exist until first commit
- `objects/` is empty until you commit
- Delete `.git` = lose all Git history

---

## Question 05: Default Branch

### What It Is
The branch automatically created when you run `git init`

### Common Defaults
- **Old default:** `master`
- **Modern default:** `main`
- **Custom:** Whatever you configure

### Key Commands
```bash
# Check current default
git config --global init.defaultBranch

# Set global default to 'main'
git config --global init.defaultBranch main

# Rename current branch
git branch -m new-name

# Rename specific branch
git branch -m old-name new-name
```

### Configuration Levels
```bash
# Local (this repo only) - Highest priority
git config --local init.defaultBranch main

# Global (your user) - Medium priority
git config --global init.defaultBranch main

# System (all users) - Lowest priority
git config --system init.defaultBranch main
```

### Important Points
- Changing default only affects NEW repos
- Existing repos keep their current branches
- Branch names are just labels (you can use any name)
- When cloning, you get the remote's default (not yours)

---

## Question 06: Purpose of .git Directory

### What Is .git?
**The `.git` directory IS the repository.** Everything else is just working files.

### Structure
```
.git/
├── HEAD              # Current branch pointer
├── config            # Repository configuration
├── index             # Staging area (after git add)
├── objects/          # THE DATABASE - all commits, files, history
│   ├── XX/           # Object storage (by hash)
│   └── pack/         # Compressed objects
├── refs/             # References
│   ├── heads/        # Local branches
│   └── tags/         # Tags
├── hooks/            # Automation scripts (.sample files)
└── info/
    └── exclude       # Like .gitignore but local
```

### Object Types
Git stores 3 main object types in `objects/`:
1. **Blob** - File contents
2. **Tree** - Directory structure  
3. **Commit** - Snapshot + metadata

### Key Commands
```bash
# Explore .git
ls -la .git
cat .git/HEAD
cat .git/config

# Count objects
find .git/objects -type f | wc -l

# Examine an object
git cat-file -t <hash>    # Show type
git cat-file -p <hash>    # Show content

# Show all Git files
find .git -type f
```

### Critical Facts
- `.git` contains ALL your repository data
- Working files are separate (just copies from `.git`)
- Delete `.git` = lose ALL history (irreversible!)
- Backup `.git` = backup entire repository
- Moving project folder = fine (`.git` moves with it)

### Working Directory vs Repository
```
Project Folder
├── .git/          ← REPOSITORY (the actual Git database)
│   └── objects/   ← All commits, all versions, all history
└── file.txt       ← WORKING FILE (current checkout from .git)
```

---

**Print this page and keep it handy while practicing!**
