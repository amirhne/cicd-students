# Git Cherry-Pick Command Documentation

## What does git cherry-pick do?

Git cherry-pick allows you to apply a specific commit from one branch to another branch. It creates a new commit on your current branch with the same changes as the picked commit, but with a different commit hash.

## Basic Usage

```bash
git switch main
git cherry-pick 2773758
```

This switches to the `main` branch and applies the changes from commit `2773758`.

## Common Use Cases

- Applying a bug fix from one branch to another without merging the entire branch
- Moving specific features between branches
- Recovering commits from deleted branches

## Cherry-Picking Multiple Commits

```bash
# Pick a range of commits
git cherry-pick A^..B

# Pick multiple specific commits
git cherry-pick commit1 commit2 commit3
```

## Handling Conflicts

If conflicts occur during cherry-pick:

```bash
# Resolve conflicts in your editor, then:
git add .
git cherry-pick --continue

# Or abort the cherry-pick:
git cherry-pick --abort
```

## Useful Options

- `--no-commit` - Apply changes without committing (allows you to modify before committing)
- `-x` - Append a line noting which commit was cherry-picked (useful for tracking)
- `-e` - Edit the commit message before committing

```bash
git cherry-pick -x 2773758
```

## Tips

Cherry-pick should be used sparingly and only as a last resort. Here's why:

**When Cherry-Pick is Appropriate:**
- Applying isolated, independent commits that don't rely on other changes
- Backporting critical bug fixes to production branches
- Selectively pulling in specific features that aren't yet part of the main development flow

**Best Practices:**
- Fix bugs directly on the main/production branch first, then merge those fixes into development branches
- Prefer merging or rebasing entire feature branches over cherry-picking individual commits
- Avoid cherry-picking commits that are part of a dependent chain, as this can lead to conflicts and broken functionality

**Why Cherry-Pick Can Be Problematic:**
- Creates duplicate commits with different hashes, making history harder to track
- Can introduce subtle bugs if dependencies between commits are overlooked
- Makes it difficult to understand the true lineage of changes
- May cause merge conflicts when the original branch is eventually merged