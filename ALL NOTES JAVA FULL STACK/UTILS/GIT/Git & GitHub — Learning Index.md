- **Module 1: Git & GitHub Fundamentals**
  1. **Version Control Basics**
     - **What is Version Control (VCS)**
     - **Centralized vs Distributed VCS**
     - **Why Git**
  2. **Git Overview**
     - **History (BitKeeper → Git, Linus Torvalds, 2005)**
     - **Git Characteristics (non-linear dev, distributed, cryptographic auth, pluggable merge strategies)**
  3. **Core Concepts / Key Terms**
     - **Repository**
     - **Working Directory**
     - **Staging Area**
     - **Commit**
     - **Branch**
     - **Merge**
     - **Clone**
     - **Fork**
     - **Remote (origin vs upstream)**
     - **HEAD**
       - **Detached HEAD state**
     - **SSH Protocol**
  4. **GitHub Basics**
     - **What is GitHub**
     - **GitHub vs Git**
     - **GitHub vs GitLab vs Bitbucket**
     - **Creating a GitHub Account**
     - **Repository Setup**
       - **Public vs Private**
       - **README**
       - **License**
       - **.gitignore**
     - **Repository Tabs**
       - **Code**
       - **Issues**
       - **Pull Requests**
       - **Projects**
       - **Wiki**
       - **Security**
       - **Insights**
       - **Settings**
  5. **Branching (Web Interface)**
     - **Creating a Branch**
     - **Branch Workflow**
     - **Committing via Web Editor**
     - **Pull Requests**
       - **Creating a PR**
       - **Reviewing a PR**
       - **Approving a PR**
     - **Merging**
       - **Regular Merge**
       - **Squash Merge**
     - **Branch Lifecycle / Cleanup**

  **Module 2: Git Commands & Workflows**
  1. **Setting Up Git**
     - **git init**
     - **git clone**
     - **git config (user.name, user.email)**
     - **git version**
  2. **Local Workflow**
     - **git status**
     - **git add**
       - **specific file / all files**
     - **git commit**
     - **git diff**
     - **git log**
  3. **.gitignore**
     - **Purpose**
     - **Syntax basics**
     - **Common patterns**
  4. **Branching & Switching**
     - **git branch (list/create/delete)**
     - **git checkout**
     - **git switch (modern alternative)**
  5. **Merging & Rebasing**
     - **git merge**
     - **git rebase**
       - **Merge vs Rebase (when to use which)**
     - **git cherry-pick**
     - **Merge Conflicts**
       - **Why they happen**
       - **Conflict markers (<<<<<<<, =======, >>>>>>>)**
       - **Manual resolution**
       - **git rerere**
  6. **Stashing**
     - **git stash**
     - **git stash pop / apply**
     - **git stash list / drop**
  7. **Remote Repositories**
     - **git remote (add/list/rename/remove)**
     - **git fetch**
     - **git pull**
     - **git push**
     - **origin vs upstream terminology**
  8. **Undoing Changes**
     - **git restore**
     - **git reset (soft/mixed/hard)**
     - **git revert**
     - **Difference: reset vs revert**
  9. **Tagging**
     - **git tag**
     - **Lightweight vs Annotated tags**
     - **Use in releases/versioning**
  10. **Cloning vs Forking**
      - **Cloning workflow**
      - **Forking workflow**
      - **Keeping a fork in sync (upstream remote)**
      - **When to use which**
  11. **Roles in GitHub Projects**
      - **Developer**
      - **Integrator**
      - **Repository Administrator**
  12. **Advanced / Patch-Based Workflows** ***(low priority, awareness-level)***
      - **git format-patch**
      - **git send-email**
      - **git am**
      - **git request-pull**
      - **git daemon / git instaweb**
  13. **GitHub Copilot** ***(awareness-level)***
      - **What it is**
      - **Typical workflow**
