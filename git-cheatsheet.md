# Git Cheatsheet

```bash
git status                      # what changed?
git switch -c my-branch         # new branch
git add <file>                  # stage a file
git commit -m "Short message"   # save a snapshot
git push -u origin my-branch    # first push of a branch
git pull                        # get latest changes
git log --oneline               # history
```

## The loop
branch -> edit -> add -> commit -> push -> open PR -> CI -> review -> merge

## Commit messages
Start with a verb, keep it short: `Add guess counter`, `Fix off-by-one in loop`.

## Never
- Commit directly to `main`
- Edit the provided tests
- Commit passwords or tokens
