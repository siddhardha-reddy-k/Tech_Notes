## **Topic 7: Local Workflow**

**git status**

Shows the current state of your working directory and staging area — what's changed, what's staged, what's untracked.

Output tells you three categories:

- **Untracked files** — new files Git has never seen before (not staged, not committed)

- **Changes not staged for commit** — files Git already tracks, but you've modified them since the last commit

- **Changes to be committed** — files sitting in the staging area, ready for the next commit

**Habit tip (worth noting for yourself):** run git status constantly — before and after every add/commit. It's the "where am I" command, costs nothing, and prevents most beginner mistakes (like committing the wrong files).

**git add**

Moves changes from the working directory into the staging area.

```bash
git add <file>       # stage one specific file
git add .             # stage everything in current directory and below
git add -A            # stage everything in the entire repo (even outside current dir)
```

**Gotcha (****.** **vs** **-A****):** git add . only stages changes in the current directory downward. If you're in a subfolder and something changed elsewhere in the repo, . won't catch it — -A stages the whole repo regardless of where you're standing. Minor but has tripped people in interviews as a "what's the difference" question.

**git commit**

Takes everything in the staging area and saves it as a permanent snapshot in history.

```bash
git commit -m "your message here"
```

- -m lets you write the message inline; without it, Git opens your default text editor

- Only what's **staged** gets committed — anything modified-but-not-added is left out

- Each commit gets a unique SHA-1 hash, records author/timestamp (from git config), and links to its parent commit

**Commit message conventions** (from your source notes, and genuinely asked about in interviews sometimes):

- Keep the summary line under ~50 characters

- Use active/imperative voice: "Add login validation" not "Added login validation" or "Adds login validation"

- Don't end the summary line with a period

- Use a blank line + longer description below if more detail is needed

**git diff**

Shows line-by-line differences — what exactly changed, not just which files.

```bash
git diff                  # unstaged changes vs last commit
git diff --staged         # staged changes vs last commit
git diff HEAD~1 HEAD      # differences between two specific commits
git diff <file>           # diff limited to one file
```

**Gotcha:** plain git diff (no flags) only shows **unstaged** changes. Once you git add a file, it disappears from plain git diff output — you need --staged (or --cached, same thing) to see staged changes. This trips people up: "I ran diff and it shows nothing, but status says I have changes" → usually means everything's already staged.

**git log**

Shows commit history.

git log                   # full history, newest first
git log -p                # includes the actual diff of each commit
git log --oneline         # condensed, one line per commit — very commonly used
git log -p filename        # history of one specific file

- Each entry shows: commit hash, author, date, message

- --oneline is what you'll actually use day-to-day for a quick glance — full git log output is verbose



**Mental model recap for this whole topic:**

```bash
git status  → "what state am I in?"
git add     → working dir → staging area
git commit  → staging area → permanent history
git diff    → "what exactly changed?" (before staging, or before committing)
git log     → "what's the history?"
```
