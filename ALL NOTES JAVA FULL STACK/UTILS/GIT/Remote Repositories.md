## **Topic 12: Remote Repositories**

You already know the concepts (origin/upstream from Topic 3) — this is the concrete command layer on top.

**git remote**

Manages connections to remote repositories — think of it as your address book of "other copies of this project."

```bash
git remote -v                              # list all remotes with their URLs (fetch + push)
git remote add origin <URL>                # add a new remote named "origin"
git remote add upstream <URL>              # add a second remote named "upstream"
git remote rename origin new-name           # rename a remote
git remote rm <name>                       # remove a remote connection
git remote show origin                      # detailed info about a specific remote
```

- A remote is just a **name + URL pair** — origin and upstream are conventions, not special keywords Git enforces

- git clone auto-adds origin for you (Topic 6) — you only manually add a remote when starting from git init, or adding a second remote like upstream when working with forks

**git fetch**

Downloads new commits/branches from a remote — **but does not merge them** into your local branches. It just updates your local view of "what's on the remote."

```bash
git fetch origin
git fetch upstream main
```

- Safe operation — never changes your working files or current branch

- After fetching, you can inspect what changed (git diff main origin/main) before deciding to merge

- Think of it as "check for updates" without "install updates"

**git pull**

Fetches **and immediately merges** remote changes into your current local branch, in one step.

```bash
git pull origin main
```

- Effectively: git fetch + git merge combined

- **Gotcha (very commonly tested):** because pull auto-merges, if your local branch has diverged from the remote, you can get a merge commit — or a conflict — without warning, since it happens in one command. Some teams prefer fetch + manual merge/rebase for more control over exactly what happens.

- There's also git pull --rebase, which fetches then rebases instead of merges — keeps history linear instead of creating merge commits on every pull

**git push**

Uploads your local commits to a remote branch.

```bash
git push origin <branch-name>
git push -u origin <branch-name>     # -u sets upstream tracking, so future pushes can just be `git push`
```

- -u (or --set-upstream) links your local branch to the remote branch permanently — after this, you can just type git push / git pull with no arguments and Git knows where to send/receive

- **Gotcha:** if the remote has commits you don't have locally (e.g., a teammate pushed first), your push gets **rejected** — Git won't let you overwrite history you haven't seen. You need to pull (or fetch + merge/rebase) first, resolve any conflicts, then push.

**origin vs upstream — in practice now**

Recall from Topic 3: convention, not enforced by Git. Concretely, in a **fork workflow**:

```bash
git clone <your-fork-URL>              # auto-creates "origin" = your fork
git remote add upstream <original-URL>  # manually add "upstream" = the original repo
```

```bash
git fetch upstream                      # get latest from the original project
git merge upstream/main                 # bring those changes into your local main
git push origin main                    # push your updated main to YOUR fork
```

This is the standard "keep my fork in sync" loop — you'll use this a lot if you contribute to open-source projects.



**Quick recap table:**

| **Command** | **Downloads?** | **Merges automatically?** | **Changes your branch?** |
| --- | --- | --- | --- |
| git fetch | Yes | No | No |
| git pull | Yes | Yes | Yes |
| git push | N/A (uploads) | N/A | Updates remote, not local |
