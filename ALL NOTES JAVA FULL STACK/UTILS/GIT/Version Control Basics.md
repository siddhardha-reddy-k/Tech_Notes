## **Topic 1: Version Control Basics**



**What is Version Control (VCS)**

  - A system that tracks changes to files over time — so you can see what changed, who changed it, and roll back if something breaks.

  - Think of it like Google Docs' "version history," but built for code, and far more powerful — it tracks changes across an entire project (hundreds of files), not just one document.

  - Without VCS: you'd be manually saving project\_final.py, project\_final\_v2.py, project\_final\_v2\_ACTUAL\_FINAL.py — chaos, no way to know what changed between versions, and no safe way for 5 people to edit the same file at once.

  - With VCS: every change is a tracked, timestamped snapshot with a description. Multiple people can work on the same codebase without overwriting each other.



  - **Centralized vs Distributed VCS**

This is the core interview distinction — **know this cold**.

|  | **Centralized (e.g., old SVN)** | **Distributed (Git)** |
| --- | --- | --- |
| Where's the history? | One central server only | Every developer has the *full* history, locally |
| Need network to commit? | Yes | No — commit locally, push later |
| If server dies? | You lose everything (unless backed up) | Every clone is a full backup |
| Speed | Slower (network round-trip for most ops) | Fast (most ops are local) |
|  |  |  |

**Gotcha:** "Distributed" doesn't mean "no central server exists" — GitHub *is* a central server. It means every local copy is a **complete, independent repository** with full history, not just a checkout of files. GitHub is just the commonly-agreed-upon "official" remote — Git doesn't require it.



**Why Git (specifically)**

Quick context on the "why" behind Git's design, since you like knowing the mechanics:

Git was built in 2005 by Linus Torvalds because the Linux kernel team lost free access to BitKeeper (the VCS they were using). Linux development had unusual demands: thousands of contributors, extremely high patch volume, no single point of trust. This shaped Git's core traits:

  - **Speed** — most operations are local, no network needed

  - **Distributed by design** — no single point of failure

  - **Strong integrity** — every commit is checksummed (SHA-1 hash), so history can't be silently altered

  - **Support for non-linear workflows** — thousands of branches/patches happening in parallel

**Interview one-liner if asked "why Git over other VCS":** *"Git is distributed, so every developer has a full local history, enabling offline work, fast operations, and no single point of failure — plus cryptographic integrity via commit hashing."*
