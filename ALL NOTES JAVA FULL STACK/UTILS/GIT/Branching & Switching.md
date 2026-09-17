## **Topic 9: Branching & Switching**

**git branch**

Lists, creates, renames, or deletes branches.

git branch                    # list all local branches (\* marks current one)
git branch -a                  # list ALL branches, including remote-tracking ones
git branch \<name\>              # create a new branch (does NOT switch to it)
git branch -d \<name\>           # delete a branch (safe — refuses if unmerged changes exist)
git branch -D \<name\>           # force delete (deletes even if unmerged — use carefully)
git branch -m \<old\> \<new\>      # rename a branch

**Gotcha (repeating from Topic 3 since it's important):** git branch \<name\> only **creates** the branch — it doesn't move you onto it. A lot of beginners create a branch, start editing files, and are confused when git status still shows they're on main. You need checkout/switch after.

**git checkout**

The "classic," multi-purpose command — switches branches, but also does other things (which is exactly why it's confusing and why git switch/git restore were introduced to split its responsibilities).

```bash
git checkout <branch-name>            # switch to an existing branch
git checkout -b <new-branch-name>     # create AND switch in one step (very commonly used)
git checkout <commit-hash>            # switch to a specific commit → DETACHED HEAD (Topic 3)
git checkout -- <file>                # discard changes in a file (old syntax, now git restore)
```

**Why checkout is considered "messy":** it does branch-switching, commit-checkout, *and* file-discarding, all with the same command name — just different arguments. Git split these into clearer commands later (switch for branches, restore for files), but checkout still works and is still extremely common in the wild, so you need to know both old and new.

**git switch (modern alternative)**

Introduced specifically to make branch-switching unambiguous — does **only** branch operations, nothing else.

```bash
git switch <branch-name>       # switch to an existing branch
git switch -c <new-branch>     # create AND switch (same as checkout -b)
git switch -                   # switch back to the previous branch (handy shortcut)
```

**Interview-relevant comparison:**

|  | **git checkout** | **git switch** |
| --- | --- | --- |
| Purpose | Multi-purpose (branches, commits, files) | Branches only |
| Ambiguity | Can be confusing — same command, many behaviors | Clear, single responsibility |
| Age | Original, still universally used | Newer (Git 2.23+), increasingly preferred |
| Detached HEAD risk | Yes, if you check out a commit hash directly | Also possible, but syntax makes intent clearer |

**Practical answer if asked "which should I use":** switch is cleaner/preferred for new work, but you'll see checkout everywhere in older code, tutorials, and probably your training program's material — know both.



**Quick recap combining Topics 3 + 9:**

```bash
git branch <name>        # create (doesn't move you)
git checkout <name>      # move you there (old way)
git switch <name>        # move you there (new way)
git checkout -b <name>   # create + move, one step (old way)
git switch -c <name>     # create + move, one step (new way)
```
