# Question 01: Working Directory, Staging Area, and Repository

## 📝 Question
What is the difference between a working directory, staging area, and repository?

## 🎯 Learning Objectives
By completing this exercise, you will understand:
- The three main areas where your files live in Git
- How files move between these areas
- Why this three-stage process exists

## 🔍 Concept Overview

Git has three main areas:

### 1. **Working Directory** 
- Your actual project folder on your computer
- Where you edit, create, and delete files
- Files here can be modified freely

### 2. **Staging Area (Index)**
- A preparation area between working directory and repository
- You select which changes you want to commit
- Think of it as a "draft" of your next commit

### 3. **Repository**
- The `.git` folder where Git stores all committed history
- Permanent record of your project's snapshots
- Once committed, changes are saved in project history

### Visual Flow
```
Working Directory  →  Staging Area  →  Repository
   (modify)         (git add)        (git commit)
```

## 💻 Hands-On Exercise

### Setup
1. Make sure you're in the `question-01` folder
2. Initialize a new Git repository

```bash
cd question-01
git init
```

### Task 1: Create Files in Working Directory
Create three files:

```bash
echo "This is file 1" > file1.txt
echo "This is file 2" > file2.txt
echo "This is file 3" > file3.txt
```

**Check status:**
```bash
git status
```

**Question:** In which area are these files now? _________________

### Task 2: Move Files to Staging Area
Add only `file1.txt` to staging:

```bash
git add file1.txt
git status
```

**Question:** What color is file1.txt? What about file2.txt and file3.txt? 
- file1.txt: _________________
- file2.txt & file3.txt: _________________

Now add file2.txt:
```bash
git add file2.txt
git status
```

### Task 3: Commit to Repository
Commit the staged files:

```bash
git commit -m "Add file1 and file2"
git status
```

**Question:** Where are file1.txt and file2.txt now? _________________

**Question:** What about file3.txt? _________________

### Task 4: Modify a Tracked File
Edit file1.txt:

```bash
echo "This is updated content" > file1.txt
git status
```

**Question:** Is file1.txt in staging area or working directory? _________________

### Task 5: Practice the Complete Flow
Now practice the complete flow:

1. Stage file3.txt
2. Stage the modified file1.txt
3. Commit both with message "Add file3 and update file1"
4. Check status

```bash
git add file3.txt file1.txt
git commit -m "Add file3 and update file1"
git status
```

## ✅ Check Your Understanding

Answer these questions:

1. **Can you commit a file directly from working directory to repository without staging?**
   - Answer: _________________

2. **Why does Git have a staging area instead of committing directly?**
   - Answer: _________________

3. **If you modify a file after staging it, do you need to stage it again before committing?**
   - Answer: _________________

## 🎓 Challenge Exercise

1. Create a file `notes.txt`
2. Add it to staging
3. Modify it before committing
4. Check git status - you should see it in both staged and unstaged!
5. Figure out how to see the difference between what's staged and what's in working directory

**Hint:** Use `git diff` and `git diff --staged`

## 📚 Solution

Ready to check your work? See [SOLUTION.md](./SOLUTION.md)

## 🔗 Next Steps
Once you've mastered this, move to [Question 02: What is HEAD in Git?](../question-02/)
