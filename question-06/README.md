# Question 06: Purpose of the .git Directory

## 📝 Question
What is the purpose of the `.git` directory?

## 🎯 Learning Objectives
By completing this exercise, you will understand:
- What the `.git` directory contains
- Why each component exists
- How Git uses `.git` to track your project
- What happens if you modify or delete `.git`
- The difference between working directory and repository

## 🔍 Concept Overview

### What is the `.git` Directory?

The `.git` directory is **the actual Git repository**. Everything else is just your working files.

**Key Concept:**
```
Your Project Folder
├── .git/           ← This IS the repository (all Git data)
├── file1.txt       ← Your working files
├── file2.txt       ← Your working files
└── folder/         ← Your working files
```

**Critical Understanding:**
- `.git` = The database of all commits, branches, history
- Your files = Current checkout from that database
- Delete `.git` = Delete all Git history (files remain, history gone)

### Why is it Hidden?

The `.` prefix makes it hidden on Unix-like systems:
- Prevents accidental deletion
- Keeps your working directory clean
- You rarely need to look inside (Git manages it)

## 💻 Hands-On Exercise

### Setup: Create a Fresh Repository

```bash
cd ~/Desktop
mkdir git-directory-study
cd git-directory-study
git init
```

### Task 1: Explore the .git Directory

List all contents:

```bash
ls -la .git
```

**Question:** How many items do you see? _________________

**List all items you see:**
1. _________________
2. _________________
3. _________________
4. _________________
5. _________________

### Task 2: Examine Each Component

#### A) HEAD - Your Current Position

```bash
cat .git/HEAD
```

**Question:** What does it say? _________________

**Purpose:** Points to your current branch

#### B) config - Repository Settings

```bash
cat .git/config
```

**Question:** What sections do you see (e.g., `[core]`)? _________________

**Purpose:** Stores repository-specific configuration

#### C) objects/ - The Database

```bash
ls .git/objects
```

**Question:** What do you see inside? _________________

**Purpose:** Stores all Git objects (commits, trees, blobs)

#### D) refs/ - Branch and Tag References

```bash
ls .git/refs
ls .git/refs/heads
ls .git/refs/tags
```

**Question:** What's inside refs/heads/? _________________

**Purpose:** Stores branch pointers

#### E) hooks/ - Automation Scripts

```bash
ls .git/hooks
```

**Question:** How many sample files are there? _________________

**Question:** What extension do they have? _________________

**Purpose:** Scripts that run at specific Git events

### Task 3: Create Content and Watch .git Grow

Create and commit a file:

```bash
echo "First file" > file1.txt
git add file1.txt
```

Check what appeared:

```bash
ls .git
```

**Question:** Did a new file appear? (Hint: look for `index`) _________________

**Purpose of index:** The staging area!

Now commit:

```bash
git commit -m "Add file1"
```

Explore objects:

```bash
ls .git/objects
```

**Question:** How many subdirectories exist now? _________________

Check refs:

```bash
ls .git/refs/heads
cat .git/refs/heads/master
# or: cat .git/refs/heads/main
```

**Question:** What's inside this file? _________________

**Answer:** A commit hash! This is where the branch points.

### Task 4: Understanding Object Storage

Make a few more commits:

```bash
echo "Second file" > file2.txt
git add file2.txt
git commit -m "Add file2"

echo "Third file" > file3.txt
git add file3.txt
git commit -m "Add file3"
```

Count objects:

```bash
find .git/objects -type f | wc -l
```

**Question:** How many objects are there? _________________

**Estimate:** Should be around 9+ objects (3 commits × 3 objects each)

Examine an object:

```bash
# Get a commit hash
git log --oneline

# Pick the first hash and examine it
git cat-file -t <commit-hash>
git cat-file -p <commit-hash>
```

**Question:** What type is it? _________________

**Question:** What information does it contain? _________________

### Task 5: The info/ and hooks/ Directories

Check info folder:

```bash
ls .git/info
cat .git/info/exclude
```

**Question:** What is this file for? _________________

Check a hook sample:

```bash
cat .git/hooks/pre-commit.sample
```

**Question:** What language is it written in? _________________

**Purpose:** This would run before every commit (if activated)

### Task 6: Understand What's NOT in .git

Your working files are separate:

```bash
ls
# Shows: file1.txt, file2.txt, file3.txt

ls .git/objects
# Shows: Git's internal object database
```

**Question:** Can you read your file contents directly in .git/objects? _________________

**Try it:**
```bash
# Try to find file1.txt content
find .git/objects -type f -exec file {} \;
```

**Question:** Are the files readable? _________________

**Answer:** No! They're compressed. Git stores them efficiently.

### Task 7: Delete .git and See What Happens

**Warning:** This is destructive (for learning only!)

```bash
# Check current state
git status
git log --oneline

# List files
ls

# Delete .git
rm -rf .git

# Try Git commands
git status
```

**Question:** What error do you get? _________________

**Question:** Are your working files (file1.txt, etc.) still there? _________________

**Question:** Can you see your commit history? _________________

### Task 8: The Difference Between Repository and Working Directory

Re-initialize:

```bash
git init
git status
```

**Question:** Does Git know about file1.txt, file2.txt, file3.txt? _________________

**Why/Why not?** _________________

**Understanding:**
- The files exist in your working directory
- But the `.git` database is new (empty)
- Previous commits are gone forever

## ✅ Check Your Understanding

### Question 1: Is .git a file or directory?

**Answer:** _________________

### Question 2: Where is the actual Git repository?

Choose one:
- A) Your working files
- B) The `.git` directory
- C) The remote server (GitHub)
- D) All of the above

**Answer:** _________________

### Question 3: What happens if you accidentally commit a secret and want to remove it from history?

**Think:** If you just delete the file and commit, is the secret gone from `.git`?

**Answer:** _________________

### Question 4: Can you move a repository to a different folder?

```bash
# Try it:
cd ~/Desktop
mkdir new-location
mv git-directory-study new-location/
cd new-location/git-directory-study
git status
git log
```

**Question:** Does Git still work? _________________

**Why?** _________________

### Question 5: What's the difference between these?

```bash
cp -r myproject myproject-backup          # Command A
cp -r myproject/.git myproject-backup/    # Command B
```

**Which one backs up your Git history?** _________________

## 🎓 Challenge Exercises

### Challenge 1: Explore Object Types

```bash
# Create a repository with commits
cd ~/Desktop
mkdir object-study
cd object-study
git init

echo "File A" > a.txt
git add a.txt
git commit -m "Commit A"

# Find all objects
find .git/objects -type f

# For each object, check its type
# Replace <hash> with actual values
git cat-file -t <hash>
```

**Question:** What types do you find? (blob, tree, commit, tag)

**Count:**
- Blobs: _________________
- Trees: _________________
- Commits: _________________

### Challenge 2: Manually Create a .git Backup

```bash
# Create a project
cd ~/Desktop
mkdir backup-test
cd backup-test
git init
echo "Important" > data.txt
git add data.txt
git commit -m "Important commit"

# Backup only .git
cp -r .git ../git-backup

# Simulate disaster
rm -rf .git
rm data.txt

# Restore from backup
cp -r ../git-backup .git
git status
git checkout .
```

**Question:** Did you recover your files? _________________

**Question:** Did you recover your commits? _________________

### Challenge 3: Compare .git Size

```bash
cd ~/Desktop
mkdir size-test
cd size-test
git init

# Check .git size
du -sh .git

# Add a large file
dd if=/dev/zero of=largefile.bin bs=1M count=10
git add largefile.bin
git commit -m "Add large file"

# Check size again
du -sh .git

# Delete the file and commit
git rm largefile.bin
git commit -m "Remove large file"

# Check size again
du -sh .git
```

**Question:** Is .git smaller after deleting the file? _________________

**Why/why not?** _________________

## 📚 Solution

Ready to check your work? See [SOLUTION.md](./SOLUTION.md)

## 🔗 Congratulations!

You've completed Questions 04-06! You now understand:
- ✅ What `git init` does internally
- ✅ Default branches and how to change them
- ✅ The purpose of the `.git` directory

### Your Progress
- ✅ Question 01: Working Directory, Staging Area, Repository
- ✅ Question 02: What is HEAD in Git?
- ✅ Question 03: Tracked vs Untracked Files
- ✅ Question 04: What does git init do?
- ✅ Question 05: Default branch in Git
- ✅ Question 06: Purpose of .git directory

**Keep practicing!** More questions coming soon.

---

## 💡 Quick Reference

### .git Directory Structure
```
.git/
├── HEAD              # Current branch pointer
├── config            # Repository config
├── description       # For GitWeb
├── hooks/            # Automation scripts
├── info/             # Additional info
│   └── exclude       # Like .gitignore
├── objects/          # THE DATABASE
│   ├── pack/         # Compressed objects
│   └── XX/           # Object storage
├── refs/             # References
│   ├── heads/        # Branches
│   └── tags/         # Tags
└── index             # Staging area (after git add)
```

### Key Takeaways
- `.git` = The repository
- Working files = Separate from repository
- Delete `.git` = Lose all history
- `.git/objects` = All your data
- `.git/refs` = Branch pointers
