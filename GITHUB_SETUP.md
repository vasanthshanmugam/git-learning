# GitHub Setup Instructions

## Step 1: Create Repository on GitHub

1. Go to https://github.com/vasanthshanmugam
2. Click the **"+"** button (top right) → **"New repository"**
3. Fill in details:
   - **Repository name:** `git-learning`
   - **Description:** "Hands-on Git learning repository with practical exercises"
   - **Visibility:** Public (so others can learn too!)
   - **DO NOT** initialize with README (we already have one)
4. Click **"Create repository"**

## Step 2: Push Your Local Repository to GitHub

GitHub will show you commands. Use these:

```bash
cd /home/claude/git-learning

# Add GitHub as remote origin
git remote add origin https://github.com/vasanthshanmugam/git-learning.git

# Rename branch to main (optional, modern convention)
git branch -M main

# Push to GitHub
git push -u origin main
```

### Alternative: If you prefer 'master' branch name
```bash
git push -u origin master
```

## Step 3: Verify on GitHub

1. Refresh your GitHub repository page
2. You should see:
   - README.md displayed on the main page
   - All question folders (question-01, question-02, question-03)
   - Commit history

## Step 4: Make It Look Professional

### Add Topics (Tags)
On your GitHub repo page:
1. Click the ⚙️ (settings icon) next to "About"
2. Add topics: `git`, `learning`, `tutorial`, `beginner-friendly`, `hands-on`
3. Save

### Add a Description
In the same "About" section, add:
"Learn Git through hands-on exercises. Master working directory, staging area, HEAD, and file tracking concepts."

### Enable Discussions (Optional)
- Settings → Features → Enable Discussions
- Great for learners to ask questions!

## Step 5: Share It!

Your repository will be live at:
```
https://github.com/vasanthshanmugam/git-learning
```

Share it with:
- Twitter/LinkedIn
- Dev.to or Hashnode articles
- Reddit communities like r/learnprogramming
- Discord/Slack communities

## Troubleshooting

### Authentication Issues
If GitHub asks for credentials:

**Option 1: HTTPS with Personal Access Token**
1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate new token (classic)
3. Select scopes: `repo` (all)
4. Copy token and use as password when pushing

**Option 2: SSH (Recommended)**
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your_email@example.com"

# Copy public key
cat ~/.ssh/id_ed25519.pub

# Add to GitHub: Settings → SSH and GPG keys → New SSH key
# Then use SSH URL instead:
git remote set-url origin git@github.com:vasanthshanmugam/git-learning.git
```

### Push Rejected
If you get "rejected" error:
```bash
git pull origin main --rebase
git push origin main
```

## What's Next?

Once pushed, you can:
1. Add a nice banner image
2. Create GitHub Actions for automated checks
3. Add more questions (PRs welcome!)
4. Start recording video tutorials

## Need Help?

If you encounter issues during setup, let me know which step is causing problems!
