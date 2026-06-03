# 🎓 Git Cheat-Sheet — Roshan's Git Journey

> Built from scratch in one session. Keep this; it covers ~95% of daily Git.

## The mental model (never forget this)
- A **commit** = a permanent SNAPSHOT saved LOCALLY. (Not a push!)
- Three areas: **Working Directory** → (`git add`) → **Staging Area** → (`git commit`) → **Repository**
- **`commit` is local. `push` is remote.** Two different steps.
- `HEAD` = "you are here" pointer.
- `origin` = the nickname for your GitHub remote. `origin/master` = last-known position of GitHub's master.

---

## 1. Core loop (do this constantly)
```bash
git status                  # what's going on? (run obsessively)
git add <file>              # stage a file (put in cart)
git add .                   # stage everything changed
git commit -m "message"     # save a snapshot locally
```

## 2. Reading history
```bash
git log                     # full history (press q to quit)
git log --oneline           # compact, one line each
git log --oneline --graph --all   # visual branch graph
git diff                    # unstaged changes (working vs staging)
git diff --staged           # staged changes (what you'll commit)
git show <hash>             # a specific commit + its diff
```

## 3. Undoing things (the safety net)
```bash
git restore <file>          # discard UNSTAGED edits (permanent for that edit)
git restore --staged <file> # un-stage (keeps the edit)
git commit --amend          # fix the LAST commit (message or add a file)
git revert <hash>           # undo a commit by making a NEW opposite commit (SAFE)
git reset <hash>            # move branch backward, rewrite history (DANGEROUS)
```

## 4. Branching & merging
```bash
git branch                  # list branches (* = current)
git switch -c <name>        # create + switch to new branch
git switch <name>           # switch to existing branch
git merge <name>            # merge <name> INTO current branch
git branch -d <name>        # delete a merged branch
```
**Merge conflict?** Edit the file (remove `<<<<<<<` `=======` `>>>>>>>` markers, keep what you want) → `git add <file>` → `git commit`.

## 5. Rebasing (rewrite history — only on UNSHARED branches!)
```bash
git rebase master           # replay current branch's commits on top of master (linear history)
git rebase -i HEAD~3        # interactive: squash/reorder/edit last 3 commits
# during conflict: fix file → git add → git rebase --continue
# escape hatch: git rebase --abort
```
⚠️ **Golden rule:** never rebase commits you've already pushed/shared.

## 6. Remotes & GitHub
```bash
git remote -v               # show connected remotes
git push                    # send local commits to GitHub
git push -u origin <branch> # first push of a branch (sets up tracking)
git fetch                   # download remote changes but DON'T merge
git pull                    # fetch + merge (download AND integrate)
git clone <url>             # copy a remote repo down to a new folder
git push origin --tags      # push tags (they don't go automatically!)
```
**Pull Request** = a merge proposed on GitHub, with review/discussion, before it hits the main branch. The core team ritual.

## 7. Versioning (SemVer) & tags
Version format: **MAJOR.MINOR.PATCH** = "break . feature . fix"
- MAJOR = breaking change (`1.x.x` → `2.0.0`)
- MINOR = new feature, backward-compatible (`1.4.x` → `1.5.0`)
- PATCH = bug fix only (`1.4.2` → `1.4.3`)
```bash
git tag -a v1.0.0 -m "message"   # annotated tag on current commit
git tag                          # list tags
git show v1.0.0                  # inspect a tag
git push origin --tags           # publish tags to GitHub
```

## 8. Everyday helpers
```bash
# .gitignore — a file listing patterns Git should ignore:
#   *.log
#   secrets.env
#   node_modules/
git stash                   # park uncommitted changes, clean the working dir
git stash list              # see the shelf
git stash pop               # bring parked changes back
```

---

## The daily rhythm (burn this into muscle memory)
```
edit  →  git add  →  git commit -m "..."  →  git push
```

## Typical team workflow
```
1. git switch -c my-feature      # branch off main
2. ...work... add, commit         # make changes
3. git push -u origin my-feature  # push the branch
4. Open a Pull Request on GitHub  # request review
5. Teammates review → merge PR
6. git switch main && git pull    # bring the merged work down
7. git branch -d my-feature       # tidy up
```

## Editor escape hatches
- **vim**: `:wq` Enter = save & quit | `:q!` Enter = quit without saving
- **nano**: `Ctrl+O` Enter = save | `Ctrl+X` = exit

## When stuck / scared
- `git status` almost always tells you what to do next.
- Uncommitted work can be lost; **committed work is almost always recoverable.**
- `--abort` backs out of a stuck merge/rebase: `git merge --abort`, `git rebase --abort`.
```
```
