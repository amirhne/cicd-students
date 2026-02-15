# Git Bisect Command Documentation

## What does git bisect do?

Git bisect is a powerful debugging tool that uses binary search to efficiently find the commit that introduced a bug. Like the limit concept in calculus where you narrow down to a precise point, bisect systematically narrows down the range of commits until it pinpoints exactly where things went wrong.

## How it works

1. **Define the range**: Mark a "bad" commit (where the bug exists) and a "good" commit (where it worked)
2. **Binary search**: Git automatically checks out the middle commit between good and bad
3. **Test and mark**: You test that commit and mark it as good or bad
4. **Repeat**: Git continues halving the range until it identifies the exact commit that introduced the issue

## Basic Usage

```bash
# Start bisecting
git bisect start

# Mark current commit as bad
git bisect bad

# Mark a known good commit (e.g., a tag or commit hash)
git bisect good v1.0

# Test the code, then mark as good or bad
git bisect good   # if it works
git bisect bad    # if it's broken

# Git will continue until it finds the culprit

# End bisecting and return to original branch
git bisect reset
```

## Why it's efficient

Instead of checking every commit linearly, bisect uses binary search:
- 100 commits → ~7 tests needed
- 1000 commits → ~10 tests needed
- 10000 commits → ~14 tests needed

Just like finding a limit by progressively narrowing the interval, bisect converges on the answer logarithmically.