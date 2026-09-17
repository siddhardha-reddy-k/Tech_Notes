## **Topic 6: Setting Up Git**

**git init**

Initializes a new, empty Git repository in the current directory — creates a hidden .git folder that stores all tracking data (commits, branches, config, etc.).

```bash
git init
```

- Run this inside a folder you want to start tracking

- Optionally specify a directory: git init \<directory-name\> creates and initializes a new folder

- After this, the folder has zero commits — it's just "ready to track," nothing is tracked yet

**Gotcha:** git init doesn't stage or commit anything automatically. It just sets up the tracking infrastructure. You still need add + commit to actually save anything.

**git clone**

Downloads a **complete copy** of a remote repository — all files, all branches, entire commit history — to your local machine.

```bash
git clone <repository-url>
```

- Creates a new folder (named after the repo by default) and puts everything inside it

- Automatically sets up a remote called origin pointing back to the source you cloned from — this happens for you, you don't need git remote add after cloning

- You get all branches, but you're checked out on the default branch (usually main) initially

**Difference from** **git init****:** init = start tracking a fresh/empty project from scratch. clone = copy an *existing* project (with all its history) that already exists somewhere else.

**git config**

Sets identity and preferences Git uses when you commit — required before your first commit, or Git will error/warn.

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

- --global — applies to *every* repo on your machine (stored in ~/.gitconfig)

- Omit --global to set config for just the current repo (stored in .git/config) — useful if you use a different email for work vs personal projects

- This name/email is what shows up attached to every commit you make — it's *not* your GitHub login, just metadata baked into the commit itself

**Gotcha (real-world, common early mistake):** if you commit before setting user.email, your commits get attributed to a default/fallback identity, and worse — if that email doesn't match your GitHub account, your commits won't show your GitHub avatar/profile link on the repo, even though you pushed them. Set config first, always.

**git version**

```bash
git --version
```

(or git version)

Just confirms Git is installed and shows which version — useful for troubleshooting if a command behaves unexpectedly (some commands like switch and restore are newer and won't exist on very old Git installs).
