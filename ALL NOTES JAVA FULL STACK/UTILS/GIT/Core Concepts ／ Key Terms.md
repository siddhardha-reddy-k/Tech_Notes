## **Topic 3: Core Concepts / Key Terms**



This is the vocabulary that everything else builds on. Get these rock solid.

**The Git Workflow Areas (this is the big mental model)**

Picture **4 zones** your code moves through:

Working Directory  →  Staging Area  →  Local Repository  →  Remote Repository
                     (git add)          (git commit)          (git push)



- **Working Directory** — the actual files on your computer, where you edit. Whatever you see in your file explorer right now.

- **Staging Area** (aka "the index") — a holding zone. Files you've marked as "ready to be part of the next commit." Not saved to history yet.

- **Local Repository** — your .git folder. Once committed, it's saved to *your* local history (but not shared with anyone yet).

- **Remote Repository** — GitHub (or wherever). Only updated when you push.

**Why staging exists (common "why" question):** it lets you commit *selectively*. If you changed 5 files but only want 2 of them in this commit, you git add only those 2. Staging = a rough draft of your next commit.



- **Repository (repo) -** A project folder tracked by Git — contains all your files **plus** the hidden .git folder that stores all the history/metadata. "Repository" and ".git folder + your files" are basically synonymous.



- **Commit -** A **snapshot** of your project at a point in time, with:

  - A unique SHA-1 hash (ID)

  - A message describing the change

  - A pointer to its parent commit(s) — this is what forms the chain/history

  - Author, timestamp

**Gotcha:** A commit isn't a "diff" conceptually (though Git stores it efficiently under the hood) — think of it as "a full snapshot," not "a change." This matters for understanding revert/reset later.



- **Branch -** A movable pointer to a specific commit — not a separate copy of all your files (common misconception). When you create a branch, Git doesn't duplicate your project; it just creates a new lightweight pointer. This is *why* branching in Git is fast and cheap, unlike some older VCS tools.

  - **main** (or master) — the default/deployable branch

  - Any branch can be treated as "main" — it's convention, not a hard rule



- **HEAD -** A pointer to **where you currently are** — usually pointing at the tip of whatever branch you've checked out. Think of HEAD as "you are here" on a map. When you git checkout other-branch, HEAD moves to point at other-branch instead.



**Example Walkthrough**

1. **Start on main:**

  - **You make Commit** **1.**

  - **What** **Git shows:** **Your project files match Commit 1.**

1. **Create and switch to feature (git checkout -b feature):**

  - **Git creates a** **feature sticky note on Commit 1 and moves HEAD to point to feature.**

1. **Make a new commit (Commit 2):**

  - **Because HEAD** **points to feature, the new commit goes onto feature.**

  - **Structure:**



- **Detached** **HEAD state (gotcha topic — interview favorite)**

Normally: HEAD → branch → commit

If you check out a **specific commit** directly (git checkout \<commit-hash\>) instead of a branch name, HEAD points *directly* at that commit, not at a branch. This is "detached HEAD."

**Why it matters:** if you make new commits while in detached HEAD and then switch to another branch, those commits can become **orphaned** — unreachable and eventually garbage-collected, effectively lost — because no branch pointer was tracking them.

**Fix if you need those commits:** create a new branch right there before switching away: git branch new-branch-name (while still detached), which "saves" that commit chain under a real branch pointer.



- **Merge -** Combining the changes from one branch into another — typically feature branch → main.



- **Clone -** Downloading a **full copy** of a remote repo (all files + entire commit history) onto your local machine. Not just the latest files — the whole history.



- **Fork -** A copy of someone else's repo made **into your own GitHub account** — a server-side operation (there's no git fork command; it only exists as a GitHub website action). Used when you don't have write access to the original and want to propose changes independently.



- **Remote: origin vs upstream**

  - **origin** — conventional name for *your* remote (the one you cloned from, or your fork)

  - **upstream** — conventional name for the *original* repo (relevant when you've forked something)

These are just labels/aliases — you could name them anything, but origin/upstream is the near-universal convention.



**Remote (origin vs upstream) Example**

**Scenario:** Contributing to an open-source project via a GitHub fork.

**Setup & Actions**

1. **Fork & Clone (origin):**

  - **You fork owner/project to your account (you/project) and clone it locally.**

  - **Result: Git automatically names your personal fork origin.**

  - ***Command:*** **git clone \[**[**https://github.com/you/project.git\](https://github.com/you/project.git)**](https://github.com/you/project.git%5d(https:/github.com/you/project.git))

1. **Add** **Original Repo (upstream):**

  - **You manually link the master project so you can track its updates.**

  - **Result: You name the official source upstream.**

  - ***Command:*** **git remote add upstream \[**[**https://github.com/owner/project.git\](https://github.com/owner/project.git)**](https://github.com/owner/project.git%5d(https:/github.com/owner/project.git))

1. **Check Remotes:**

  - ***Command:*** **git remote -v**

  - ***Output:*** **Shows both origin (your workspace) and upstream (the source).**

**Daily Workflow**

- **Pull official updates (upstream):** Grab new code from the main project.
git fetch upstream
git merge upstream/main

- **Push your work (origin):** Send your completed feature to your GitHub fork to open a pull request.
git push origin feature-branch



- **SSH Protocol -** A secure method for authenticating with GitHub over the network without typing your password every time — you generate a key pair (public/private), give GitHub the public key, and Git uses your private key locally to prove it's you.
