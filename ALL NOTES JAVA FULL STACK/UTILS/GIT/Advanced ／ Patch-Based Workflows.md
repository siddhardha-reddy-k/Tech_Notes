**Topic 17: Advanced / Patch-Based Workflows** 
*(awareness-level — rarely used day-to-day, but good to recognize if it comes up)*

These commands come from Git's original design context: Linux kernel development, where contributions were often exchanged over **email**, not a web platform like GitHub (remember — Git predates GitHub by a few years, and even today some major open-source projects like the Linux kernel itself still use email-based patch workflows).

**git format-patch**

Converts one or more commits into .patch files — plain text files representing the changes, formatted so they can be emailed.

```bash
git format-patch -1 HEAD          # generate a patch file for the last commit
git format-patch main..feature     # generate patch files for all commits on feature not in main
```

**git send-email**

Sends the generated .patch files directly to a maintainer's email address, formatted properly as a patch submission.

```bash
git send-email --to=maintainer@example.com *.patch
```

**git am ("apply mailbox")**

On the receiving end — takes an incoming patch file (from email) and applies it directly to the repository as a real commit, preserving the original author/message metadata.

```bash
git am < patch-file.patch
```

**git request-pull**

Generates a text summary of your pending changes (commits, diff stats) so a maintainer can review and decide whether to pull your work — a lightweight, non-GitHub alternative to opening a formal Pull Request.

```bash
git request-pull main https://your-fork-url feature-branch
```

**git daemon / git instaweb**

- **git daemon** — runs a lightweight server exposing repos over the git:// protocol, allowing others to clone/fetch without needing SSH/HTTPS auth setup — mostly used for quick internal/local network sharing

- **git instaweb** — instantly spins up a local web interface (using a lightweight built-in web server) to browse your own repo's history in a browser, without needing GitHub at all

**Why this matters (briefly)**

**Practical reality for you:** you will almost certainly never use these day-to-day — GitHub's PR-based workflow has replaced email patches for the vast majority of teams and even most open-source projects. This section exists mainly so you **recognize the terms** if they come up in a course glossary, MCQ, or if you ever read about how the Linux kernel itself is developed (it's a famous exception — it still primarily uses git am/mailing lists rather than GitHub PRs).

**If asked in an interview:** a simple "I'm aware Git supports email-based patch workflows via format-patch/send-email/am, though most modern teams use PR-based workflows instead" is more than sufficient — no need to go deep.
