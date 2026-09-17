## **Topic 14: Tagging**

Short, low-risk topic.

**git tag**

Marks a specific commit with a permanent, human-readable label — typically used to mark **release points** (v1.0, v2.1.3, etc.). Unlike a branch, a tag doesn't move — it's a fixed pointer to one exact commit forever.

```bash
git tag                          # list all tags
git tag <tag-name>                # create a lightweight tag on the current commit
git tag <tag-name> <commit-hash>  # tag a specific past commit, not just the current one
git tag -d <tag-name>              # delete a local tag
```

**Branch vs Tag (quick distinction, sometimes asked):** a branch pointer *moves forward* automatically as you commit. A tag is *static* — it always points to the exact same commit, forever, unless manually deleted/moved.

**Lightweight vs Annotated tags**

# Lightweight — just a name pointing to a commit, no extra metadata
git tag v1.0

# Annotated — a full object with message, author, date, and (optionally) GPG signature
git tag -a v1.0 -m "Release version 1.0"

|  | **Lightweight** | **Annotated** |
| --- | --- | --- |
| Stores | Just a pointer to a commit | Tagger name, email, date, message — a real Git object |
| Use case | Quick, private/local bookmarks | Actual releases, anything shared publicly |
| Recommended for releases? | No | **Yes** — this is the standard for real releases |

**Rule of thumb (interview-safe answer):** *"Use annotated tags for anything that matters — releases, shared milestones — since they carry metadata and are the recommended standard. Lightweight tags are fine for quick, throwaway local markers."*

**Pushing tags (tags don't push automatically!)**

```bash
git push origin <tag-name>       # push a single tag
git push origin --tags            # push ALL tags at once
```

**Gotcha:** git push on its own does **not** push tags — tags are separate from commits/branches in this respect. You need an explicit --tags or name the specific tag. This surprises people who tag a release locally, push normally, and wonder why the tag isn't showing up on GitHub.

**Use in releases/versioning**

Standard practice: once a version is ready to ship, tag the exact commit (usually on main) with something like v1.2.0 (following [Semantic Versioning](https://semver.org/) — MAJOR.MINOR.PATCH). GitHub can turn tags into formal "Releases" on the web UI, attaching release notes/changelogs and downloadable assets to that exact snapshot.
