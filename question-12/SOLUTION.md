# Solution: git cherry-pick

## ✅ Quick Answers

### Task 1: Understanding Setup
- **Commits on feature-b:** 2 commits
- **Messages:** "Add divide function", "Update changelog for divide function"

### Task 3: Cherry-Pick
- **Worked:** YES
- **Conflicts:** Probably NO (if clean)
- **Commit on main:** YES
- **Hash different:** YES (new commit created)
- **Still on feature-b:** YES (original unchanged)

### Task 4: What Got Cherry-Picked
- **File modified:** CHANGELOG.md only
- **Divide function code:** NO
- **Only changelog:** YES

### Task 5: Compare Commits
- **Hashes identical:** NO (different commits)
- **Changes identical:** YES (same diff)

### Task 8: Cherry-Pick vs Merge
**Answer:** Likely B or C
- Cherry-picked commits are duplicates
- Git might detect this or create merge commit
- Better to cherry-pick OR merge, not both

### Task 10: When NOT to Cherry-Pick
**Should you cherry-pick feature-a?**
- **Answer:** NO, merge instead
- **Why:** Only 1-2 commits, feature is complete
- **Cherry-pick is for:** selective single commits

## Check Your Understanding - Answers

**Q1:** Copies specific commit from one branch to another
**Q2:** When you need ONE specific commit, not the whole branch
**Q3:** TRUE (new hash, same changes)
**Q4:** NO (stays on original branch)
**Q5:** "importing a whole library" / "copying one function you need"

## Common Use Cases

### 1. Hotfix Workflow
```
feature → bug fix commit
         ↓ cherry-pick
main → bug fix commit (copy)
```

### 2. Backport Fix
```
version-2.0 → security fix
             ↓ cherry-pick
version-1.0 → security fix (copy)
```

### 3. Wrong Branch Recovery
```
main → commit (oops, meant for feature)
      ↓ cherry-pick to feature
feature → commit (now here too)
```

## Key Differences

| Action | Merge | Cherry-Pick |
|--------|-------|-------------|
| **What** | Entire branch | Specific commits |
| **Creates** | Merge commit | New commit(s) |
| **History** | Preserves branch | Linear |
| **Use when** | Feature complete | Need specific fix |

## GitHub Validation Checklist

- [ ] Cherry-picked commit appears on target branch
- [ ] Original commit still on source branch
- [ ] Commit hash is different
- [ ] File changes are identical
- [ ] Network graph shows both commits

Congratulations on completing all 12 questions! 🎉
