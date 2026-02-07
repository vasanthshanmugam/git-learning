# Question 10: What is the Difference Between `git pull` and `git clone`?

## 📝 Question
What is the difference between `git pull` and `git clone`?

## 🎯 Learning Objectives
By completing this exercise, you will understand:
- When to use `git clone` vs `git pull`
- What each command does internally
- How to work with remote repositories on GitHub
- The relationship between local and remote repositories
- Real-world workflows with remote repos

## 🔍 Concept Overview

### git clone
**Purpose:** Create a local copy of a remote repository

**When to use:**
- First time getting a repository
- You don't have the code yet
- Starting work on a new project

**What it does:**
- Downloads entire repository
- Creates a new folder
- Sets up remote tracking
- Checks out default branch

### git pull
**Purpose:** Update your existing local repository with changes from remote

**When to use:**
- You already have the repository
- Someone else made changes
- You want to get the latest code

**What it does:**
- Fetches changes from remote
- Merges them into your current branch
- Updates your working directory

### Key Difference
```
git clone  = "I don't have this repo, give me everything"
git pull   = "I have this repo, give me updates"
```

## 💻 GitHub-Based Exercise

### Prerequisites

You'll need:
1. A GitHub account
2. The practice repository: `git-learning-practice-repo`

### Task 1: Fork the Practice Repository

**On GitHub:**

1. Go to: `https://github.com/vasanthshanmugam/git-learning-practice-repo`
2. Click the **"Fork"** button (top right)
3. GitHub creates a copy in your account

**Validation:**
✅ Check: Do you see the repo in your GitHub repositories?
✅ URL should be: `https://github.com/YOUR-USERNAME/git-learning-practice-repo`

**Question:** What did forking create? _________________

### Task 2: Clone the Repository (First Time)

**On Your Computer:**

Open terminal/command prompt:

```bash
cd ~/Desktop
git clone https://github.com/YOUR-USERNAME/git-learning-practice-repo.git
cd git-learning-practice-repo
```

**Validation on Your Computer:**
```bash
ls
# You should see: README.md, app.js, config.json, CHANGELOG.md, SETUP.md

git status
# Should show: "On branch main"

git remote -v
# Should show your GitHub repo URL
```

**Questions:**
- Did a new folder get created? _________________
- Can you see all the files? _________________
- What branch are you on? _________________

**Question for Understanding:** If you delete this folder and clone again, will you get the same files? _________________

### Task 3: Make Changes on GitHub (Remote)

**On GitHub Website:**

1. Go to your forked repository on GitHub
2. Click on `README.md`
3. Click the **pencil icon** (Edit this file)
4. Add this line at the bottom:
   ```
   ## My Practice Session
   Started practicing on [Today's Date]
   ```
5. Scroll down to "Commit changes"
6. Write commit message: `Update README with practice session`
7. Click **"Commit changes"**

**Validation on GitHub:**
✅ Check: Click on `README.md` - do you see your new section?
✅ Check: Click on commits - do you see "Update README with practice session"?

**Question:** Where is this change right now? (GitHub or your computer?) _________________

### Task 4: Check Local Repository (Before Pull)

**On Your Computer:**

```bash
cat README.md
```

**Question:** Do you see "My Practice Session" section? _________________

**Why/why not?** _________________

Check if Git knows about remote changes:

```bash
git status
```

**Question:** Does it say you're behind? _________________

**Why?** _________________

### Task 5: Use git pull to Get Updates

**On Your Computer:**

```bash
git pull origin main
```

**Validation:**
```bash
cat README.md
# You should now see "My Practice Session" section

git log --oneline -3
# You should see "Update README with practice session"
```

**Questions:**
- Do you now see your GitHub changes locally? _________________
- Did you need to clone again? _________________

**Understanding:** `git pull` updated your existing repository!

### Task 6: Make Local Changes and Push

**On Your Computer:**

Edit a file locally:

```bash
echo "// This change was made locally" >> app.js
git add app.js
git commit -m "Add local comment to app.js"
```

Push to GitHub:

```bash
git push origin main
```

**Validation on GitHub:**
1. Go to your GitHub repository
2. Click on `app.js`
3. Scroll to bottom

**Question:** Do you see "// This change was made locally"? _________________

### Task 7: Simulate Team Collaboration

**Scenario:** A teammate (you, using GitHub web interface) makes a change

**On GitHub:**

1. Click on `config.json`
2. Click pencil icon to edit
3. Change `"version": "1.0.1"` to `"version": "1.1.0"`
4. Commit with message: `Bump version to 1.1.0`

**On Your Computer (without pulling):**

Try to make a different change:

```bash
# Edit app.js
echo "// Another local change" >> app.js
git add app.js
git commit -m "Add another comment"

# Try to push
git push origin main
```

**Question:** Did the push work? _________________

**Question:** What error message did you get? _________________

Now pull first:

```bash
git pull origin main
git push origin main
```

**Question:** Did it work after pulling? _________________

### Task 8: Clone vs Pull Comparison

**Test Clone Again:**

```bash
cd ~/Desktop
# Create a new clone in different location
git clone https://github.com/YOUR-USERNAME/git-learning-practice-repo.git practice-clone-2
cd practice-clone-2
ls
```

**Questions:**
- Did you get all the latest changes? _________________
- Did you need to use `git pull`? _________________

**Understanding:** `git clone` always gets the latest version from GitHub!

**Try Pull on New Clone:**

```bash
git pull origin main
```

**Question:** What message did you get? _________________

**Why?** _________________

### Task 9: Understanding Remote Tracking

**On Your Computer (in original clone):**

```bash
git remote -v
```

**Question:** What URL does `origin` point to? _________________

Check branch tracking:

```bash
git branch -vv
```

**Question:** What does it say about `main` branch tracking? _________________

**Understanding:** Your local `main` tracks `origin/main` on GitHub!

### Task 10: The Complete Workflow

**Validation Exercise - Do This Sequence:**

1. **On GitHub:** Edit `CHANGELOG.md`, add entry "Practice completed"
2. **On Computer:** Run `git pull origin main`
3. **Verify:** `cat CHANGELOG.md` shows your addition
4. **On Computer:** Create new file: `echo "Done!" > practice-complete.txt`
5. **On Computer:** `git add practice-complete.txt && git commit -m "Mark practice complete"`
6. **On Computer:** `git push origin main`
7. **On GitHub:** Verify `practice-complete.txt` exists

**Validation Checklist:**
- [ ] Can see "Practice completed" in CHANGELOG.md locally
- [ ] Can see "Practice completed" in CHANGELOG.md on GitHub
- [ ] Can see practice-complete.txt on GitHub
- [ ] All commits show in GitHub commit history

## ✅ Check Your Understanding

### Question 1: When do you use git clone?

**Answer:** _________________

### Question 2: When do you use git pull?

**Answer:** _________________

### Question 3: Complete the analogy

"`git clone` is like _________________ a library, while `git pull` is like _________________ books you already borrowed."

**Answer:** _________________

### Question 4: What happens if you run git clone on a folder that already exists?

**Answer:** _________________

### Question 5: Can you use git pull without first using git clone?

**Answer:** _________________

**Why/why not?** _________________

## 🎓 Challenge Exercises

### Challenge 1: Multiple Remotes

**On GitHub:**
1. Fork the practice repo again to a different account (or use original repo)

**On Your Computer:**
```bash
git remote add upstream https://github.com/vasanthshanmugam/git-learning-practice-repo.git
git remote -v
```

**Question:** How many remotes do you have now? _________________

Try pulling from upstream:
```bash
git pull upstream main
```

**Question:** What happened? _________________

### Challenge 2: Clone to Specific Folder

```bash
cd ~/Desktop
git clone https://github.com/YOUR-USERNAME/git-learning-practice-repo.git my-custom-folder
ls
```

**Question:** What's the folder name? _________________

### Challenge 3: Pull from Specific Branch

**On GitHub:**
1. Go to `feature-a` branch
2. Make any change
3. Commit it

**On Your Computer:**
```bash
git checkout -b feature-a origin/feature-a
git pull origin feature-a
```

**Validation on GitHub:**
Go to branches tab and verify your changes

## 📚 Solution

Ready to check your work? See [SOLUTION.md](./SOLUTION.md)

## 🔗 Next Steps

Once you understand clone vs pull, move to [Question 11: Fast-forward vs Three-way Merge](../question-11/)

---

## 💡 Quick Reference

### git clone
```bash
# Clone a repository
git clone https://github.com/username/repo.git

# Clone to specific folder
git clone https://github.com/username/repo.git folder-name

# Clone specific branch
git clone -b branch-name https://github.com/username/repo.git
```

### git pull
```bash
# Pull from tracked branch
git pull

# Pull from specific remote and branch
git pull origin main

# Pull and rebase instead of merge
git pull --rebase origin main
```

### Check Remote
```bash
git remote -v              # View remotes
git remote add name url    # Add remote
git branch -vv             # Check tracking branches
```

## 🎯 Key Takeaways

| Command | Use Case | What It Does |
|---------|----------|--------------|
| `git clone` | First time | Downloads entire repo, creates folder |
| `git pull` | Get updates | Fetches and merges changes into existing repo |

**Remember:**
- Clone = Getting the repo for the first time
- Pull = Updating the repo you already have
- Always pull before pushing!
