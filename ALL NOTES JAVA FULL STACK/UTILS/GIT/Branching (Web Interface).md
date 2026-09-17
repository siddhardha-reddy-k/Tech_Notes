## **Topic 5: Branching (Web Interface)**

This is doing via GitHub's website what we'll later do via CLI in Module 2 — good to know both, since some teams do quick edits via web UI.

**Creating a Branch (Web)**

- Click the branch dropdown (usually shows "main")

- Type a new branch name → select "Create branch: name from main"

- The new branch starts as an **exact copy** of main at that moment — same files, same history up to that point

**Naming convention tip** (not in your source doc, but standard practice, worth noting for your notes): branch names are usually descriptive and sometimes prefixed by type — feature/product-recommendation, fix/login-bug, hotfix/payment-crash. Makes it obvious at a glance what a branch is for.



**Branch Workflow (Web)**

- Multiple branches can be worked on simultaneously by different people — they don't interfere with each other until merged

- To edit a file on a branch: select the file → pencil icon (edit) → make changes → commit **directly to that branch** (web editor asks which branch to commit to)



**Committing via Web Editor**

- After editing, scroll to "Commit changes"

- Add a commit message (required) + optional extended description

- Choose: commit directly to the current branch, **or** create a new branch and start a PR (GitHub offers this if you're editing a branch you don't have direct write access to



**Pull Requests (PRs)**

**Purpose:** propose merging one branch into another, with a review step before it happens.

**Creating a PR**

- Go to "Pull Requests" tab → "New pull request"

- Choose the **base** branch (usually main) and the **compare** branch (your feature branch)

- GitHub shows a diff of all changes

- Add title + description → "Create pull request"

**Gotcha:** a PR can be opened even if the branch isn't finished — this is intentional. Opening early lets teammates see work-in-progress and comment before it's "done." (This is sometimes called a **draft PR** on GitHub specifically.)

**Reviewing a PR**

- Reviewers see the diff, can comment on specific lines, approve, request changes, or reject

- GitHub keeps an **immutable log** of who approved what — audit trail for accountability

**Approving a PR**

- At least one approval is typically required (enforced via branch protection rules, which live in Settings)

- Once approved, the "Merge" button becomes active



**Merging**

**Regular Merge**

- Creates a **merge commit** — a new commit with two parents (the tip of main + the tip of the feature branch)

- Preserves full branch history — you can see exactly which commits came from the feature branch

**Squash Merge**

- Combines **all** commits from the feature branch into a **single** commit on main

- Keeps main's history clean/linear — useful when a feature branch has messy commits like "wip", "fix typo", "actually fix it"

**Interview-relevant comparison:**

|  | **Regular Merge** | **Squash Merge** |
| --- | --- | --- |
| History | Preserves every commit from branch | Collapses into 1 commit |
| main branch history | Can get noisy | Stays clean/linear |
| Traceability | Full detail of dev process | Less granular — just "feature X added" |

There's also **rebase merge** (mentioned in GitHub's PR options) — replays your branch's commits on top of main instead of creating a merge commit. We'll cover rebase properly in Topic 10 since it's more of a CLI concept — just know GitHub's PR merge button offers 3 options: Merge, Squash, Rebase.

**Branch Lifecycle / Cleanup**

- Once a branch is merged and no longer needed, **delete it** (GitHub even shows a "Delete branch" button right after merge)

- Keeps the repo's branch list clean — old stale branches pile up fast on active projects and make navigation confusing
