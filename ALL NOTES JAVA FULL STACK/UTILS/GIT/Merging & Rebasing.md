## **Topic 10: Merging & Rebasing**

This is the meatiest topic — merge vs rebase is one of the most common Git interview questions. Take your time with this one.

**git merge**

Combines changes from one branch into another by creating a new commit (a "merge commit") that has **two parents**.

bash

```bash
git checkout main
git merge feature-branch
```

- You merge *into* whatever branch you're currently on

- If main hasn't changed since the feature branch split off, Git does a **fast-forward merge** — no merge commit needed, main just moves its pointer forward

- If both branches have diverged (both have new commits since the split), Git creates a **merge commit** with two parent commits — this is what preserves full branch history

**Fast-forward vs true merge**

Fast-forward (main unchanged):          True merge (both changed):
main:    A---B                          main:    A---B-------M
                \\                                    \\      /
feature:         C---D                  feature:      C---D
(main just moves to D)                  (M = merge commit, 2 parents)

**git rebase**

Takes your branch's commits and **replays** them on top of another branch's latest commit — rewriting history to look linear, as if you'd branched off *now* instead of earlier.

bash

```bash
git checkout feature-branch
git rebase main
```

Before rebase:                 After rebase:
main:    A---B---E              main:    A---B---E
              \\                                    \\
feature:       C---D            feature:             C'---D'
                                 (C and D recreated as C', D' — new hashes)

**Merge vs Rebase — THE core comparison (memorize this table)**

|  | **Merge** | **Rebase** |
| --- | --- | --- |
| History | Preserves exact history, including a merge commit | Rewrites history — linear, no merge commit |
| Commit hashes | Original commits stay unchanged | Commits get **new hashes** (they're recreated) |
| Safety on shared branches | Safe — never rewrites existing commits | **Dangerous on shared/pushed branches** — rewrites history others may have already pulled |
| Resulting log | Can look "messy" with merge bubbles | Clean, straight-line history |
| Use case | Team collaboration, public branches | Cleaning up your own local branch before sharing |

**The golden rule (very commonly asked):** *"Never rebase a branch that others are already working on / that's already been pushed and pulled by others."* Since rebase rewrites commit hashes, anyone who already has the old commits will get massive conflicts when they try to sync — their history and yours no longer match.

**Good rebase use case:** you're on a solo feature branch with messy commits ("wip", "fix", "fix again") — rebase onto latest main to clean things up and get a straight line, *before* pushing/sharing it.

**git cherry-pick**

Applies **one specific commit** from another branch onto your current branch — without merging the whole branch.

bash

```bash
git cherry-pick <commit-hash>
```

**Use case:** a bug fix was committed on a feature branch, but you need that exact fix on main right now, without pulling in the rest of the unfinished feature. Cherry-pick grabs just that one commit.

**Merge Conflicts**

**Why they happen**

Git can auto-merge changes to different lines/files. A conflict happens when **the same lines** were changed differently in both branches (or one branch modified a line, the other deleted it) — Git can't decide which version is "correct," so it stops and asks you.

**Conflict markers**

When a conflict occurs, Git edits the file directly, inserting markers around the conflicting section:

\<\<\<\<\<\<\< HEAD
your current branch's version of this line
=======
the incoming branch's version of this line
\>\>\>\>\>\>\> feature-branch

**Manual resolution steps**

1. Open the file, find the conflict markers

1. Decide what the final code should be — keep one side, the other, or a combination

1. **Delete the markers themselves** (\<\<\<\<\<\<\<, =======, \>\>\>\>\>\>\>) — a common beginner mistake is forgetting to remove them

1. Stage the resolved file: git add \<file\>

1. Complete the merge: git commit (Git auto-generates a merge commit message, or you can edit it)

If mid-rebase instead of merge, the flow is slightly different: git add \<file\> then git rebase --continue (not git commit — rebase handles that differently). Also useful: git merge --abort or git rebase --abort if you want to bail out entirely and return to the pre-conflict state.

**git rerere ("Reuse Recorded Resolution")**

An opt-in feature that **remembers how you resolved a conflict** and automatically reapplies that same resolution if the identical conflict shows up again (common in long-lived branches that get rebased repeatedly).

bash

```bash
git config --global rerere.enabled true
```

Niche but worth knowing exists — mostly relevant in advanced/long-running branch workflows, not something you'll use daily as a beginner.



**Interview one-liner if asked "merge vs rebase, which do you use":** *"I use merge for shared/public branches to preserve accurate history, and rebase to clean up my own local commits before pushing — never rebase something others have already pulled."*
