## **Topic 13: Undoing Changes**

This is a high-stakes topic — reset --hard in particular is one of the few commands that can actually **destroy work permanently**. Pay close attention to the gotchas here.



**git restore**

The modern, focused command for discarding changes in your **working directory or staging area** — does not touch commit history at all.

bash

```bash
git restore <file>              # discard uncommitted changes in working directory (back to last commit)
git restore --staged <file>     # unstage a file (move it from staging back to working dir, keeps the edits)
```

- git restore \<file\> = "throw away my edits to this file, go back to how it was at last commit" — **destructive** for that file's uncommitted changes, but doesn't touch history

- git restore --staged \<file\> = "I staged this by mistake, take it back out of staging" — **non-destructive**, your edits are still there, just unstaged

This replaces the older, more confusing git checkout -- \<file\> syntax (still works, but restore is clearer about intent).

**git reset**

Moves your current branch pointer to a different commit — with three modes controlling what happens to your staging area and working directory.

bash

git reset --soft \<commit\>     # move branch pointer only — staging + working dir untouched
git reset --mixed \<commit\>    # move pointer + unstage everything — working dir untouched (this is the DEFAULT if you omit a flag)
git reset --hard \<commit\>     # move pointer + unstage + DISCARD all working directory changes



**The three modes explained concretely**

Say you're at commit C and run git reset \<commit-B\>:

| **Mode** | **Branch pointer** | **Staging area** | **Working directory (your files)** |
| --- | --- | --- | --- |
| --soft | Moves to B | Keeps everything from C staged | Unchanged — files still show C's content |
| --mixed (default) | Moves to B | Cleared — C's changes become unstaged | Unchanged — files still show C's content |
| --hard | Moves to B | Cleared | **Reverted to B — all changes since B are gone** |

**Common practical use — undo last commit but keep the changes to redo it:**

bash

```bash
git reset --soft HEAD~1     # "uncommit" but keep everything staged, ready to recommit
```

**⚠****️** **THE BIG GOTCHA:** git reset --hard HEAD~1 (or any hard reset) **permanently deletes** **uncommitted work** in your working directory — no confirmation prompt, no undo (well, git reflog can sometimes recover it within a limited window, but don't rely on that). This is the single most dangerous everyday Git command. If ever unsure, use --soft or --mixed first — you can always go harder later, but you can't easily go back.

**git revert**

Undoes a commit by creating a **brand new commit** that reverses its changes — history is never rewritten, nothing is deleted.

bash

```bash
git revert <commit-hash>
git revert HEAD              # revert the most recent commit
```

- Safe for shared/pushed branches, since it *adds* to history instead of rewriting it

- If teammates have already pulled the commit you're undoing, revert is the only safe option — reset would rewrite history they already have, causing the same danger discussed in rebase (Topic 10)



**reset vs revert — THE core comparison (frequently asked)**

|  | **git reset** | **git revert** |
| --- | --- | --- |
| History | Rewrites/removes commits | Preserves history, adds a new "undo" commit |
| Safe on shared branches? | **No** — dangerous if others have pulled | **Yes** — always safe |
| Use case | Local, unpushed mistakes | Undoing something already pushed/shared |
| Can lose work? | Yes, with --hard | No — it's additive |

**Interview one-liner:** *"Reset rewrites history and is only safe for local commits you haven't shared. Revert creates a new commit that undoes changes, so it's safe to use even on commits others already have."*



**Quick decision guide for yourself:**

- Made a typo in your last commit message, haven't pushed? → reset --soft HEAD~1, fix, recommit

- Committed the wrong files, haven't pushed? → reset --mixed HEAD~1, fix staging, recommit

- Need to completely nuke local changes and start over from a known-good commit, haven't pushed? → reset --hard (carefully)

- Need to undo something that's **already pushed and others may have pulled**? → revert, never reset --hard
