# Solution: Fast-Forward vs Three-Way Merge

## ✅ Quick Answers

### Task 1: Starting State
- **Branches:** main, feature-a, feature-b, hotfix (4 branches)
- **Main commits:** 2 (Initial + Setup instructions)

### Task 3: Fast-Forward Merge
- **Commits added:** 1 (the hotfix commit)
- **Merge commit created:** NO
- **History linear:** YES
- **What happened:** main pointer moved forward to hotfix's commit

### Task 5: Three-Way Merge Setup
- **feature-a has main's new commit:** NO (branches diverged)
- **main has commits feature-a doesn't:** YES
- **feature-a has commits main doesn't:** YES

### Task 7: Three-Way Merge
- **Merge commit created:** YES ("Merge pull request...")
- **Parent commits:** 2 (one from main, one from feature-a)

### Task 8: Compare Merges
- **Hotfix (fast-forward):** Straight line, no merge node
- **Feature-a (three-way):** Lines converge, merge node present

## Key Differences Summary

| Type | Creates Commit | History | Use Case |
|------|---------------|---------|----------|
| Fast-Forward | NO | Linear | Simple updates, hotfixes |
| Three-Way | YES | Branched | Feature development, collaboration |

## Check Your Understanding - Answers

**Q1:** Fast-forward happens when target branch has no new commits
**Q2:** Three-way happens when both branches have new commits
**Q3:** B) Three-way only
**Q4:** "moves the branch pointer" / "a new merge commit"
**Q5:** Three-way merge (shows merge commit with two parents)

## Visual Comparison

**Fast-Forward:**
```
Before: main → A → B
              hotfix → B → C

After:  main → A → B → C
```

**Three-Way:**
```
Before: main → A → B → C
            feature → B → D → E

After:  main → A → B → C → M
                    feature → D → E
```

## GitHub Validation

- **Network graph** clearly shows the difference
- **Merge commits** have multiple parent commits
- **Fast-forward** appears as linear progression
- **PR history** indicates merge type

Continue to Question 12!
