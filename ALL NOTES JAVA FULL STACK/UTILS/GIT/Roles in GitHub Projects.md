## **Topic 16: Roles in GitHub Projects**

Short, conceptual — mostly for awareness, occasionally shows up in MCQs about "who does what."

**Developer**

The person writing code, working within their own branch/fork, contributing changes upward.

**Typical commands used:**

- git clone — get the project locally

- git pull / git fetch — stay updated with the remote

- git push — send local commits to the shared remote

- git request-pull — generates a summary of pending changes to ask a maintainer to pull your work (older/CLI-native workflow, less common with GitHub's PR UI but still conceptually relevant)

**Integrator**

Sits above developers — receives contributions, reviews them, and decides what gets folded into the "official" codebase.

**Responsibilities:**

- Reviews and responds to pull requests

- Merges approved changes

- Publishes/pushes the integrated result so it's available to everyone else

- Can undo problematic merges if something breaks

**Typical commands used:**

- Everything a Developer uses, **plus**:

- git pull — to merge in trusted contributors' changes

- git revert — to safely undo a bad merge/commit without rewriting shared history (ties back to Topic 13 — revert is the *safe* undo, which is exactly why an integrator managing a shared branch uses it instead of reset)

- git push — to publish the integrated, reviewed result

**Repository Administrator**

Not primarily about writing code — about **structuring and governing** the repo/project itself.

**Responsibilities:**

- Sets up and maintains access control (who can read/write/admin)

- Structures the repo — categories, organization, relationships between projects

- Configures automation — GitHub Actions for CI/CD (tying back to earlier mentions of Continuous Integration/Continuous Delivery)

- Manages settings like branch protection rules (e.g., "require PR review before merge to main" — this is literally what enforces the Developer→Integrator review flow)

- Handles server/documentation/email/index configuration in larger self-hosted setups

**Note:** this role uses far fewer direct Git commands day-to-day — it's mostly GitHub Settings/Actions/access-control work, not CLI-heavy.

**Quick summary table**

| **Role** | **Focus** | **Key Commands** |
| --- | --- | --- |
| Developer | Writing code | clone, pull, fetch, push, request-pull |
| Integrator | Reviewing & merging | (all Developer commands) + revert |
| Repo Admin | Governance & config | Mostly GitHub Settings/Actions, not CLI |

**Why this matters practically for you:** in your training/interview context, this maps directly onto real team structure — as a fresher, you'll almost always start purely as a **Developer** (branch, commit, push, open PR), while senior engineers or leads act as Integrators, and DevOps/team leads handle the Administrator role.
