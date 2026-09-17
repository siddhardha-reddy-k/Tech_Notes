**Topic 2: Git Overview** (quick, since we already covered most of this in Topic 1)



**History (BitKeeper → Git)**

- Early 2000s: Linux kernel devs used **BitKeeper**, free to use.

- 2005: BitKeeper revoked free access after a dispute with a developer who tried to reverse-engineer it.

- Linus Torvalds needed a replacement **fast** — Linux couldn't function without some VCS. He built Git in about **10 days** of initial core work.

- Named "Git" — Torvalds jokingly said it's British slang for an unpleasant person, and "I name all my projects after myself" (self-deprecating joke).

**Git's Design Characteristics (interview-relevant)**

These are the specific engineering goals Git was built around — worth memorizing as a list since "what makes Git different" is a common question:

1. **Speed** — local operations, no server round-trip

1. **Simple design**

1. **Strong support for non-linear development** — thousands of parallel branches (Linux got **6.7 patches/sec** at peak — insane concurrency to support)

1. **Fully distributed** — every clone = full repo with complete history

1. **Efficient with large projects** — Linux kernel itself is huge

1. **Cryptographic authentication of history** — every commit gets a SHA-1 hash based on its content + parent commit. If any past commit is altered, its hash changes, breaking the chain — so tampering is detectable.

1. **Pluggable merge strategies** — Git doesn't force one way to resolve merges; different strategies can be swapped in for complex cases.

**Gotcha to watch for in MCQs:** People confuse "Git" and "GitHub." Git = the *version control tool* (works entirely offline, no account needed). GitHub = a *company/website* that hosts Git repos online and adds collaboration features (PRs, issues, etc.) on top. You could use Git your whole life and never touch GitHub.
