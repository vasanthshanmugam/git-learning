# Question 04: What Does `git init` Do Internally?

## 📝 Question
What does `git init` do internally?

## 🎯 Learning Objectives
By completing this exercise, you will understand:
- What happens when you run `git init`
- The internal structure Git creates
- What each component in `.git` folder does
- How Git stores your repository data

## 🔍 Concept Overview

### What is `git init`?

`git init` transforms a regular folder into a Git repository. It's the command that "turns on" Git for a project.

**What it does:**
- Creates a hidden `.git` folder
- Sets up Git's internal database structure
- Initializes the default branch
- Prepares the repository to track changes

**Important:** After `git init`, your folder becomes a Git repository, but no files are tracked yet.

## 💻 Hands-On Exercise

### Setup: Create a Fresh Practice Folder

**DO NOT** do this inside the git-learning folder. Create a new folder elsewhere:

```bash
# Navigate to your Desktop or Documents
cd ~/Desktop

# Create a practice folder
mkdir git-init-practice
cd git-init-practice
```

### Task 1: Explore Before Git Init

Check what's in the empty folder:

```bash
ls -la
```

**Question:** How many items do you see? _________________

**Question:** Do you see a `.git` folder? _________________

### Task 2: Run Git Init

Initialize Git:

```bash
git init
```

**Question:** What message does Git show you? _________________

**Question:** What is the name of the branch it mentions? _________________

### Task 3: Discover the .git Folder

List all files again:

```bash
ls -la
```

**Question:** Do you see `.git` now? _________________

**Question:** What type is it? (file or directory?) _________________

### Task 4: Explore .git Directory Structure

Let's see what's inside:

```bash
ls .git
```

**Question:** How many items are in the `.git` folder? _________________

**Question:** List at least 5 items you see:
1. _________________
2. _________________
3. _________________
4. _________________
5. _________________

### Task 5: Explore Important Components

#### A) The HEAD File

```bash
cat .git/HEAD
```

**Question:** What does HEAD point to? _________________

#### B) The config File

```bash
cat .git/config
```

**Question:** What section do you see (like `[core]`)? _________________

#### C) The objects Directory

```bash
ls .git/objects
```

**Question:** How many subdirectories do you see? _________________

**Question:** Do you see any files with commit hashes yet? _________________

#### D) The refs Directory

```bash
ls .git/refs
ls .git/refs/heads
```

**Question:** What's inside `refs/heads/`? _________________

### Task 6: Understanding What Git Init Created

Let's verify what `git init` set up:

```bash
# Check repository status
git status
```

**Question:** What does Git say about the branch? _________________

**Question:** Does Git show any commits yet? _________________

### Task 7: See Git Init in Action - Create Content

Now let's see how Git uses these structures:

```bash
# Create a file
echo "Hello Git" > file.txt

# Check status
git status

# Stage and commit
git add file.txt
git commit -m "First commit"
```

Now explore again:

```bash
# Check objects folder
ls .git/objects
```

**Question:** Do you see more subdirectories now? _________________

**Explanation:** Git created objects to store your commit!

```bash
# Check refs/heads
cat .git/refs/heads/master
# (or main, depending on your default)
```

**Question:** What's in this file now? _________________

**Explanation:** This is the commit hash of your first commit!

### Task 8: Verify HEAD Connection

```bash
cat .git/HEAD
```

**Question:** Does HEAD still point to the same branch? _________________

```bash
# Show the commit HEAD points to
git show HEAD
```

**Question:** Does this show your "First commit"? _________________

## ✅ Check Your Understanding

### Question 1: What would happen if you deleted the .git folder?

Try it (in your practice folder):
```bash
rm -rf .git
git status
```

**Answer:** _________________

**Explanation:** Without `.git`, Git doesn't know this is a repository!

Re-initialize:
```bash
git init
```

**Question:** Are your previous commits still there? _________________

**Why?** _________________

### Question 2: Can you have nested Git repositories?

Create a subfolder and try:
```bash
mkdir subfolder
cd subfolder
git init
```

**Question:** Does this work? _________________

**Question:** How many .git folders do you have now? _________________

**Is this a good idea?** _________________

### Question 3: What's the difference between these commands?

```bash
git init
git init myproject
```

Try the second one:
```bash
cd ~/Desktop
git init test-project
ls
cd test-project
ls -la
```

**Answer:** _________________

## 🎓 Challenge Exercises

### Challenge 1: Explore Object Storage

After making a commit, explore the objects:

```bash
# List all object directories
find .git/objects -type f

# Pick one hash and try to read it (they're compressed)
# Example: if you see .git/objects/a1/b2c3d4...
git cat-file -p a1b2c3d4

# Replace with actual hash from your repo
```

**Question:** What type of object is it? _________________

### Challenge 2: Manual HEAD Change

**Warning:** This is experimental - for learning only!

```bash
# Create a new branch
git branch experiment

# Manually change HEAD
echo "ref: refs/heads/experiment" > .git/HEAD

# Check status
git status
```

**Question:** What branch are you on now? _________________

**Question:** Did you use `git checkout`? _________________

Switch back:
```bash
git checkout master
# or: git checkout main
```

### Challenge 3: Compare Fresh vs. Used Repo

```bash
# Create another test repo
cd ~/Desktop
mkdir test-repo-2
cd test-repo-2
git init

# Compare .git/objects
ls .git/objects

# Now make 3 commits
echo "A" > a.txt && git add a.txt && git commit -m "A"
echo "B" > b.txt && git add b.txt && git commit -m "B"
echo "C" > c.txt && git add c.txt && git commit -m "C"

# Check objects again
ls .git/objects
```

**Question:** How many more subdirectories appeared? _________________

**Question:** Can you explain why? _________________

## 📚 Solution

Ready to check your work? See [SOLUTION.md](./SOLUTION.md)

## 🔗 Next Steps
Once you understand git init, move to [Question 05: Default Branch in Git](../question-05/)

---

**Important Notes:**
- The `.git` folder contains ALL your repository data
- Never manually edit files in `.git` (except for learning!)
- Deleting `.git` = losing all Git history
- Each Git repository has its own `.git` folder
