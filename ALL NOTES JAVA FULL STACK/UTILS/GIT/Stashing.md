## **Topic 11: Stashing**

Short, practical topic — good to know but low depth.

**The Problem It Solves**

You're mid-way through editing files on a branch, uncommitted, and suddenly need to switch branches (urgent bug fix, checkout main, etc.) — but Git won't let you switch cleanly if it would overwrite your uncommitted changes. You don't want to commit half-finished work just to switch away. **Stash** is the answer: temporarily "shelve" your changes without committing them.



**git stash**

Saves your uncommitted changes (staged + unstaged) to a hidden stack, and reverts your working directory back to match the last commit — clean slate.

bash

```bash
git stash                    # stash all tracked changes
git stash save "message"     # stash with a descriptive label (older syntax)
git stash -u                  # also stash untracked files (not included by default)
```

Now you can safely switch branches, do whatever's urgent, then come back.



**git stash pop / apply**

Brings your stashed changes back.

bash

```bash
git stash pop          # reapply the most recent stash AND remove it from the stash list
git stash apply         # reapply the most recent stash but KEEP it in the stash list
```

**Gotcha (common "what's the difference" question):** pop = apply + delete from stash in one step. apply = apply only, stash entry stays around — useful if you want to apply the same stashed changes to *multiple* branches without re-stashing each time.



**git stash list / drop**

bash

```bash
git stash list                  # see all stashed entries (you can have multiple)
git stash drop stash@{0}        # delete a specific stash entry without applying it
git stash clear                  # delete ALL stashes
```

Stashes are stacked — stash@{0} is the most recent, stash@{1} the one before that, etc. git stash and git stash pop with no index always act on stash@{0}.



**Mental model:** stash = a clipboard for uncommitted work. Cut it out (stash), go do something else, paste it back (pop/apply) when ready.

**Interview framing:** *"**When would you use git stash?"* → "When I need to switch context quickly — like an urgent fix on another branch — without committing incomplete work."
