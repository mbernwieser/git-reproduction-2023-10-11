**Reproduction:**

```
# create new branch from initial main
git branch branch-1

# on main
echo "change" >> a/1
git add a/1 && git commit -m "add change to file a/1"

# on branch-1
git checkout branch-1
git mv a/1 b/1
git commit -m "Move a/1 to b/1"
cp b/1 a/1
git add a/1
git commit -m "Re-add a/1"

# on main
git checkout main
git merge branch-1
```

**Question**

Should there be conflicts when merging `branch-1` back to `main`?

**Result**

- No merge conflicts
- After the merge a/1 and b/1 are out of sync

**Reset after first run:**

```
git reset --hard $(git rev-list --max-parents=0 --abbrev-commit HEAD)
git branch -D branch-1
```