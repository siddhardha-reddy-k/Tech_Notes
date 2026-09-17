## **Topic 15: Cloning vs Forking**

Mostly consolidation — you've already got the pieces from Topics 3 and 12. This ties it together into one clean picture.

**Cloning workflow**

```bash
git clone <repository-url>
```

- Creates a full local copy (all files + entire history) of a repo you **already have access to** (either it's public, or you're a collaborator with write access)

- origin is auto-set to point back to that repo

- Straightforward: clone → branch → commit → push (directly, since you have access)

**Use when:** you're a collaborator on a team project with direct write access to the repo.



**Forking workflow**

- A **GitHub-only** action (no git command) — creates a copy of someone else's repo **into your own GitHub account**

- Used when you **don't** have write access to the original repo and want to propose changes independently

# 1. Fork via GitHub website (button click)
# 2. Clone YOUR fork locally
git clone \<your-fork-url\>          # origin = your fork automatically

# 3. Add the original repo as a second remote
git remote add upstream \<original-repo-url\>

# 4. Work normally
git checkout -b my-feature
# ...make changes...
git add .
git commit -m "Add feature"
git push origin my-feature          # push to YOUR fork, not the original

# 5. Open a Pull Request FROM your fork's branch TO the original repo (via GitHub website)

**Use when:** contributing to open-source projects, or any repo where you lack direct write access.



**Keeping a fork in sync (upstream remote) — full recap**

Your fork doesn't auto-update when the original repo changes. You have to manually pull those changes in:

```bash
git fetch upstream                  # get latest commits from the original repo
git merge upstream/main             # merge them into your local main
git push origin main                # push the updated main back to YOUR fork
```

(Or git pull upstream main to fetch + merge in one step, same as Topic 12.)

**Why this matters practically:** if you fork a project and don't sync for months, your fork drifts far behind — when you eventually open a PR, it may have tons of conflicts unrelated to your actual change. Regular syncing keeps PRs clean.

**Cloning vs Forking — the core comparison (interview** **favorite)**

|  | **Clone** | **Fork** |
| --- | --- | --- |
| What it creates | Local copy on your machine | Server-side copy on **your GitHub account** |
| Requires write access to original? | Yes (to push back directly) | **No** — that's the whole point |
| Git command? | Yes — git clone | **No** — GitHub website only |
| Typical next step | Branch, commit, push directly | Branch, commit, push to fork, then open PR to original |
| Use case | Team members on the same project | Outside contributors / open source |

**One-liner if asked "clone vs fork, what's the difference"****:** *"Cloning downloads a local copy of a repo you already have access to. Forking creates your own remote copy on GitHub, used when you don't have write access and need to propose changes via a pull request."*
