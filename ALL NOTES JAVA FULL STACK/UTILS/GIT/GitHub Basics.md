## **Topic 4: GitHub Basics**

**What is GitHub**

A web-based hosting service for Git repositories, owned by Microsoft. Adds a UI + collaboration layer (issues, PRs, project boards, actions) on top of plain Git.

**GitHub vs Git — the one-liner**

**Git** = the version control tool (works fully offline, no account needed).

**GitHub** = a company/platform that hosts Git repos online and adds collaboration tooling.

You already nailed this distinction in Topic 2 — just reinforcing since it's a very common "explain the difference" interview question.

**GitHub vs GitLab vs Bitbucket**

|  | **GitHub** | **GitLab** | **Bitbucket** |
| --- | --- | --- | --- |
| Owner | Microsoft | GitLab Inc. | Atlassian |
| Known for | Largest community, open source hub | Built-in DevOps/CI-CD platform (all-in-one) | Tight Jira/Trello integration |
| CI/CD | GitHub Actions | GitLab CI/CD (very mature, built-in) | Bitbucket Pipelines |

**Interview note:** don't overthink this — you just need to know they're all Git hosting platforms with different ecosystems/integrations. GitLab is often cited as having the strongest built-in CI/CD.

**Creating a GitHub Account**

Sign up → verify email → choose free/pro/team plan. Nothing conceptually deep here — just know the account is where repos and organizations live.

**Organization** vs **personal account**: an org is a shared account multiple people can own repos under, with role-based access control (admin, member, etc.) — used for companies/teams.

**Repository Setup**

- **Public vs Private** — public: anyone can view (clone/fork depends on further settings); private: only invited collaborators can see it.

- **README** — README.md, the landing page description of the project. Shown automatically on the repo homepage.

- **License** — legal terms for how others can use/modify/distribute your code (MIT, Apache 2.0, GPL are common ones).



**.gitignore -** A file listing patterns for files/folders Git should **never track** — e.g., build artifacts, dependency folders (node\_modules/), secrets/.env files, IDE config folders.

**Why it matters (practical + interview):**

- Keeps repo clean (no junk/generated files)

- Prevents accidentally committing secrets (API keys, passwords)

- Prevents committing huge folders like node\_modules or venv

**Basic syntax:**

\*.log           # ignore all .log files
node\_modules/   # ignore this folder entirely
.env            # ignore this specific file
build/          # ignore build output folder
!important.log  # exception — DO track this one file even though \*.log is ignored

**Gotcha:** .gitignore only works on **untracked** files. If a file is already committed/tracked, adding it to .gitignore won't stop Git from tracking it — you have to explicitly untrack it first:

```bash
git rm --cached <file>
```

This is a real interview trap question: *"I added a file to .gitignore but Git still tracks changes to it — why?"*

## **Repository Tabs (web interface)**

- **Code** — the actual files, default landing tab

- **Issues** — bug tracking / task tracking, not directly tied to code changes

- **Pull Requests** — proposed changes awaiting review/merge

- **Projects** — Kanban-style boards for planning

- **Wiki** — freeform documentation pages

- **Security** — vulnerability alerts, dependency scanning

- **Insights** — analytics: contributors, commit activity, traffic

- **Settings** — repo name, visibility, access control, branch protection rules, webhooks
