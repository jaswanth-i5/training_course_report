# Git Detailed Report

## 1. Introduction to Git

### 1.1 What is Git?

Git is a **Version Control System (VCS)**. It helps you:

- **Track changes** made to your files (usually source code).
- **Save different versions** of your work without creating multiple folders like `project_v1`, `project_final`, etc.
- **Collaborate** with others on the same project without conflicting code.

Git acts like a **time machine and teamwork tool**—allowing you to go back in time, undo mistakes, and work in parallel safely.

### 1.2 Why Do We Need Git?

| Without Git                          | With Git                                     |
| ------------------------------------ | -------------------------------------------- |
| Manual backups like `file_final2.py` | Changes tracked using commits                |
| Cannot undo mistakes easily          | Can go back to older versions                |
| Sharing code via email or drives     | Fast collaboration using remote repositories |
| Code conflicts often                 | Branching eliminates conflicts               |

### 1.3 Who Created Git?

- Created by **Linus Torvalds** (creator of Linux kernel) in **2005**.
- Built for speed and handling large open-source projects like Linux.

### 1.4 How Git Works

Git is a **Distributed Version Control System (DVCS)**:

- Every developer has a **full copy of the repository**, including its entire history.
- Most operations (commit, branch, log) work **offline**.

### 1.5 Important Terms

| Term         | Meaning                                              |
| ------------ | ---------------------------------------------------- |
| Repository   | A directory tracked by Git.                          |
| Commit       | A snapshot of changes.                               |
| Staging Area | Temporary area to prepare changes before committing. |
| Branch       | Separate timeline of development.                    |
| Merge        | Combining two branches.                              |
| Clone        | Copy of remote repo.                                 |
| Push         | Upload commits to remote.                            |
| Pull         | Fetch + merge remote commits.                        |

### 1.6 Snapshots, Not Differences

Git saves **snapshots** of your entire project state at each commit. If files are unchanged, Git simply references the existing version to save space.

### 1.7 Git vs GitHub

| Feature       | Git               | GitHub                       |
| ------------- | ----------------- | ---------------------------- |
| Type          | Command-line tool | Web platform                 |
| Purpose       | Version control   | Code hosting & collaboration |
| Works Offline | Yes               | No                           |
| Created By    | Linus Torvalds    | Microsoft (bought later)     |

### 1.8 Benefits of Git

✔ Fast and efficient  
✔ Tracks everything  
✔ Safe experimentation using branches  
✔ Ideal for collaboration  
✔ Free and open-source

---

## 2. Installation and Setup

### 2.1 Installing Git

#### On Windows:

1. Go to **https://git-scm.com/**
2. Download & install → Git Bash + Git GUI included.
3. During installation:
   - Choose editor (VS Code recommended)
   - Select “Git from the command line”
   - Use HTTPS by default.

#### On macOS:

- Run `git --version`. If not installed, you'll be prompted to install Xcode tools.  
  Or install using Homebrew:

```
brew install git
```

#### On Linux:

Ubuntu/Debian:

```
sudo apt update
sudo apt install git
```

Fedora:

```
sudo dnf install git
```

### 2.2 Verify Installation

```
git --version
```

### 2.3 Configure Git (First Time Setup)

```
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

Verify using:

```
git config --global --list
```

### 2.4 Optional Recommended Settings

```
git config --global core.editor "code --wait"
git config --global color.ui auto
git config --global init.defaultBranch main
```

### 2.5 Create a Repository

#### Initialize a new repo:

```
cd project-folder
git init
```

#### Clone an existing repo:

```
git clone https://github.com/user/repo.git
```

### 2.6 `.git` Folder Structure

When you run `git init`, a hidden folder `.git/` is created containing history, logs, branches, etc. Do **not delete** it.

### 2.7 Git Help Commands

| Command              | Purpose                   |
| -------------------- | ------------------------- |
| `git help`           | List common commands      |
| `git help <command>` | Detailed manual           |
| `git commit --help`  | Help for specific command |

---

# 3. The Basics: Adding & Committing

Git tracks changes in your project through two main actions — **adding** and **committing**.  
This section explains how Git moves your files through different states and how you save changes permanently.

---

## 3.1 The Three File States in Git

| State         | Meaning                            | Command That Affects It |
| ------------- | ---------------------------------- | ----------------------- |
| **Untracked** | New file; Git doesn't track it yet | -                       |
| **Staged**    | File added to staging area         | `git add <file>`        |
| **Committed** | File changes saved in Git history  | `git commit`            |

---

## 3.2 Understanding the Git Workflow

```
Working Directory  →  Staging Area  →  Local Repository
(untracked/modified)   (git add)       (git commit)
```

---

## 3.3 Checking the Current Status

```bash
git status
```

---

## 3.4 Adding Files to Staging Area

| Command            | Description                    |
| ------------------ | ------------------------------ |
| `git add file.txt` | Adds a specific file           |
| `git add .`        | Adds all modified & new files  |
| `git add *.html`   | Adds all `.html` files         |
| `git add folder/`  | Adds all files inside a folder |

---

## 3.5 Making Your First Commit

```bash
git commit -m "Your meaningful commit message"
```

---

## 3.6 Skipping the Staging Area

```bash
git commit -am "Update header styling"
```

---

## 3.7 Viewing Commit History

```bash
git log
git log --oneline
```

---

## 3.8 Undoing a Staged File

```bash
git restore --staged <file>
# or
git reset <file>
```

---

# 4. Commit in Detail

A commit is like a **snapshot** of your project at a particular point in time. It permanently stores your staged changes in the Git repository.  
In this section, we will deeply understand how commits work, how Git stores them, and why they are so powerful.

---

## 4.1 What is a Commit?

A **commit**:

- Saves changes from the staging area to the repository.
- Records **who made the change**, **when**, and **why**.
- Creates a **unique ID (SHA-1 hash)** to track the version.

Command to make a commit:

```bash
git commit -m "Your commit message"
```

---

## 4.2 Commit Structure (What’s Inside a Commit?)

Each commit contains:
| Part | Description |
|------|-------------|
| **SHA-1 Hash** | Unique 40-character ID for the commit |
| **Author** | Name & email of the person who made the commit |
| **Timestamp** | When the commit was made |
| **Commit Message** | Description of the change |
| **Parent Commit** | The commit it is based on |
| **Snapshot** | State of the files at that moment |

Example commit in Git log:

```
commit a3f12bc67891d0f44c90ad23d91f52be3ac67efd
Author: John Doe <john.doe@example.com>
Date:   Mon Nov 3 10:15:23 2025 +0530

    Add user login feature
```

---

## 4.3 What is SHA (Secure Hash Algorithm)?

- Git uses **SHA-1 (40 hexadecimal characters)** to uniquely identify a commit.
- Example:

```
a3f12bc67891d0f44c90ad23d91f52be3ac67efd
```

- If even one character in your code changes, the SHA changes completely.

You can reference commits using:

```bash
git checkout <commit-hash>
git show <commit-hash>
```

---

## 4.4 Writing Good Commit Messages

### ✅ Best Practices:

- Use **imperative tone** (e.g., "Fix bug", not "Fixed bug")
- Be **brief but meaningful**
- First line should be **50 characters or less**
- Leave a blank line before detailed description (if needed)

### ✅ Good Example:

```
Add authentication for login system

- Implemented JWT-based login
- Added password hashing using bcrypt
- Updated user database schema
```

---

## 4.5 Staging Area (Index)

The **staging area** is where Git stores changes before committing.

| Command                         | Meaning               |
| ------------------------------- | --------------------- |
| `git add file.txt`              | Adds file to stage    |
| `git reset file.txt`            | Removes from stage    |
| `git restore --staged file.txt` | Modern way to unstage |

To commit everything in staging:

```bash
git commit -m "message"
```

---

## 4.6 Viewing a Commit in Detail

```bash
git show <commit-hash>
```

This displays:

- Author, date, message
- What lines were added or removed (diff)

---

## 4.7 Viewing Commit History

| Command                           | Description               |
| --------------------------------- | ------------------------- |
| `git log`                         | Full details of commits   |
| `git log --oneline`               | Short, single-line view   |
| `git log --graph --oneline --all` | Branch + commit tree view |

---

## 4.8 Amending the Last Commit

If you forgot to add a file or want to change the commit message:

```bash
git commit --amend
```

### Change only commit message:

```bash
git commit --amend -m "Updated message"
```

⚠ Note: Do NOT amend commits already pushed to GitHub.

---

## 4.9 Where Are Commits Stored?

Inside `.git/` folder:

- `objects/` → stores snapshots and commit data
- `refs/heads/` → stores branch pointers
- `HEAD` → points to the current branch

---

# 5. Working with Branches

Branches in Git allow you to diverge from the main line of development and continue to work without affecting the main codebase.

## 5.1 What is a Branch?

A branch is simply a movable pointer to a commit. The default branch is usually called `main` or `master`.

## 5.2 Why Use Branches?

- To work on new features safely.
- To fix bugs without affecting production code.
- To experiment with ideas.
- To collaborate with others.

## 5.3 Creating a Branch

```bash
git branch <branch-name>
```

Example:

```bash
git branch feature-login
```

## 5.4 Switching Between Branches

```bash
git checkout <branch-name>
```

or (modern way):

```bash
git switch <branch-name>
```

To create and switch to a new branch in one step:

```bash
git checkout -b <branch-name>
```

or:

```bash
git switch -c <branch-name>
```

## 5.5 Viewing Branches

| Command         | Description                        |
| --------------- | ---------------------------------- |
| `git branch`    | List all local branches            |
| `git branch -r` | List remote branches               |
| `git branch -a` | List all (local + remote) branches |

The current branch will be marked with an asterisk (\*).

## 5.6 Renaming a Branch

Rename the current branch:

```bash
git branch -m <new-name>
```

Rename any branch:

```bash
git branch -m <old-name> <new-name>
```

## 5.7 Deleting a Branch

Delete a branch that has been merged:

```bash
git branch -d <branch-name>
```

Force delete (if not merged):

```bash
git branch -D <branch-name>
```

## 5.8 Pushing a Branch to GitHub

```bash
git push -u origin <branch-name>
```

## 5.9 Pulling a Remote Branch

```bash
git fetch origin
git checkout <branch-name>
```

## 5.10 Visualizing Branches

```bash
git log --oneline --graph --all
```

Example output:

```
* a3f12bc (HEAD -> feature-login) Add login UI
* 9b71d19 (main) Fix typo in README
* 5d6a7a3 Initial commit
```

---

✅ **End of Section 5: Working with Branches**

## 6. Merging Branches

Merging is the act of combining the histories of two branches. You typically merge a feature branch into the main branch when the feature is complete.

---

### 6.1 Fast-forward vs 3-way Merge

**Fast-forward merge** happens when the target branch has not advanced since you created the feature branch.

Example:

```
main:    A --- B --- C
feature:             C --- D --- E
```

If `main` hasn't moved beyond commit `C`, merging `feature` into `main` simply moves the `main` pointer forward.

```bash
git checkout main
git merge feature   # Fast-forward: main now points to E
```

**3-way merge** happens when both branches have new commits after they diverged.

```
         D --- E   (feature)
        /
A --- B --- C --- F   (main)
```

Git uses **three points** — the common ancestor, the tip of the current branch, and the tip of the branch being merged — to create a merge commit.

```bash
git checkout main
git merge feature    # Creates a new merge commit
```

---

### 6.2 Merge Commit Example

```bash
git checkout main
git merge feature
# If no conflicts:
# Merge made by the 'recursive' strategy.
#  file.txt | 2 ++
#  1 file changed, 2 insertions(+)
```

A merge commit looks like this in the log:

```
*   m3 Merge branch 'feature' into main
|\
| * e2 Feature change
| * e1 Feature start
* | f1 Main change after branching
|/
* a0 Initial commit
```

---

### 6.3 Merge Conflicts

Merge conflicts occur when the same parts of a file are changed in different branches.

Example conflict markers:

```
<<<<<<< HEAD
line from main
=======
line from feature
>>>>>>> feature
```

**To resolve conflicts:**

1. Open the confused file and manually edit the content.
2. Stage the resolved file:
   ```bash
   git add <file>
   ```
3. Complete the merge:
   ```bash
   git commit
   ```

**Helpful commands:**

```bash
git status         # Show conflicted files
git diff           # Show conflict details
git checkout --ours <file>   # Use version from current branch
git checkout --theirs <file> # Use version from feature branch
```

---

### 6.4 Merge Strategies and Options

- **`--no-ff`** → Force a merge commit even if fast-forward is possible:

```bash
git merge --no-ff feature
```

- **`--squash`** → Combine all commits from the feature branch into a single commit on the target branch:

```bash
git checkout main
git merge --squash feature
git commit -m "Add feature (squashed)"
```

`--squash` is useful for keeping a clean, linear history with one commit per feature.

---

## 7\. Comparing using `git diff`

`git diff` shows the differences between the various states in your repo: working directory, staging area, commits, and branches.

---

### 7.1 Basic usages

- Changes in working directory (unstaged):

  `git diff`

- Changes staged for commit:

  `git diff --staged # or git diff --cached`

- Compare two branches:

  `git diff main..feature`

- Compare commits:

  `git diff <commit1> <commit2>`

- Show file-level stats:

  `git diff --stat main..feature`

---

### 7.2 Interpreting the output

```
diff --git
a/app.js
b/app.js
index 3b18e6f..b1c2f7d 100644
--- a/app.js
+++ b/app.js
@@ -10,6 +10,7 @@
-  old line
+  new line
+  another new line
```

---

### 7.3 Diff tools and formats

- Show patch for a single file:

  `git diff HEAD~1 HEAD -- path/to/file`

- Use an external diff tool:

  `git difftool main..feature`

- Colorize, word-diff:

  `git diff --word-diff`

---

## 8\. Stashing

Stash lets you temporarily shelve (stash) changes in your working directory so you can work on something else, then reapply them later.

---

### 8.1 Basic stash commands

- Save current changes:

  `git stash # or keep untracked files: git stash -u`

- List stashes:

  `git stash list # stash@{0}: WIP on feature: 7a1c23d Add feature`

- Apply the latest stash (keeps stash entry):

  `git stash apply`

- Apply and drop:

  `git stash pop`

- Drop a stash:

  `git stash drop stash@{0}`

- Clear all stashes:

  `git stash clear`

---

### 8.2 Stashing specific paths

`git stash push path/to/file.txt`
#or with message

`git stash push -m "wip: trying X" -- path1 path2`

---

### 8.3 Stash and branches

You can `git stash` on one branch, switch to another, and `git stash apply` there — useful for quickly switching contexts. Use `git stash branch <name>` to create a new branch from stash:

`git stash branch wip-branch stash@{0}`

This creates a branch and applies the stash in one command.

---

## 9\. Undoing Changes & Time Travel

Git gives multiple ways to undo changes — some rewrite history, others create new commits. Know the difference before you use them.

---

### 9.1 Local, uncommitted changes

- Discard changes in working directory (restore file to HEAD):

  `git restore <file>`

- Unstage a file:

  `git restore --staged <file> # or git reset <file>`

---

### 9.2 Undo last commit (but keep changes staged)

`git reset --soft HEAD~1`

### 9.3 Undo last commit and keep changes in working directory

`git reset --mixed HEAD~1 # shorthand: git reset HEAD~1`

### 9.4 Undo last commit and discard changes

`git reset --hard HEAD~1`

> **Warning:** `--hard` deletes uncommitted changes. Use carefully.

---

### 9.5 Create a new commit that undoes a previous commit (safe for public history)

`git revert <commit-sha>`

`git revert` is safe when the commit has been pushed to remote because it does not rewrite history — it adds a new commit that reverses changes.

---

### 9.6 Checkout vs Restore (modern commands)

- `git checkout <commit>` can switch to a commit (detached HEAD) — not recommended for undoing.
- Prefer:

  `git switch <branch>      # to change branches git restore <file>       # to restore working tree files git restore --staged <file>`

---

### 9.7 Recovering deleted branches

If you deleted a branch recently, find its tip in the reflog and recreate:

`git reflog # find commit hash git branch recovered <commit-hash>`

`git reflog` is your friend for recovering lost commits within the local repository.

---

## 10\. GitHub Basics

GitHub is a web-hosted Git service that adds collaboration features (pull requests, issues, actions) on top of Git.

---

### 10.1 Connect your local repo to GitHub

Create a repo on GitHub, then:

`git remote add origin https://github.com/you/repo.git git push -u origin main`

For SSH:

`git remote add origin git@github.com:you/repo.git git push -u origin main`

---

### 10.2 Common GitHub workflows

- **Push commits**:

  `git push origin branch-name`

- **Clone**:

  `git clone https://github.com/user/repo.git`

- **Fetch remote changes**:

  `git fetch origin`

- **Open a Pull Request (PR)**: Use GitHub UI to compare branches, add reviewers, and merge.

---

### 10.3 Pull Requests

A Pull Request is a request to merge changes from one branch into another (often from a fork/feature branch into `main`). Key parts:

- Title and description (explain _what_ and _why_)
- Reviewers (people who review the code)
- CI checks (automated tests/linters)
- Discussion and change requests
- Merge (via GitHub’s merge button)

---

### 10.4 Collaborator permissions

GitHub repos have roles: Owner, Admin, Maintainer, Contributor — access controls affect who can push and merge.

---

### 10.5 Useful GitHub features

- **Issues** for tracking bugs/features
- **Projects** (boards) for planning
- **Actions** for CI/CD workflows
- **Pages** for hosting static sites
- **Security alerts** and Dependabot for dependency updates

---

## 11\. Fetching vs Pulling

These two commands are often confused — they do different things.

---

### 11.1 `git fetch`

Downloads commits, files, and refs from remote but **does not modify your working branch**. It updates remote-tracking branches (e.g., `origin/main`).

`git fetch origin # nothing changed in your current branch, just fetched remote updates`

Check differences:

`git log --oneline --graph --decorate origin/main..main # or git status`

---

### 11.2 `git pull`

`git pull` is shorthand for `git fetch` followed by a merge (by default) — it fetches remote commits and attempts to integrate them into your current branch.

`git pull origin main # equivalent to: # git fetch origin # git merge origin/main`

If you prefer rebase instead of merge:

`git pull --rebase origin main # fetch then rebase your commits onto origin/main`

---

### 11.3 When to use which

- Use `git fetch` when you want to inspect changes before integrating.
- Use `git pull` when you want to update quickly and accept the default merge/rebase behavior.
- Many teams prefer `fetch` + manual `merge`/`rebase` to avoid surprises.

---

## 12\. GitHub Extras

This section covers additional GitHub features that help collaboration and automation.

---

### 12.1 Fork vs Clone

- **Clone**: create a local copy of a repo you have access to.
- **Fork**: create your own copy of someone else's repository on GitHub (useful for open-source contribution).

Fork → clone your fork locally → push to your fork → open PR to upstream.

---

### 12.2 Issues & Labels

Issues are tracked with labels, assignees, milestones. Use templates to standardize bug reports and feature requests.

---

### 12.3 Pull Request Templates and CODEOWNERS

- **PR templates** ensure submitters provide necessary info.
- **CODEOWNERS** file automatically request reviews from code owners.

---

### 12.4 GitHub Actions (CI/CD)

Automate testing, building, and deployment using workflow YAML files in `.github/workflows/`.

Minimal example:

`name: CI on: [push, pull_request] jobs:   build:     runs-on: ubuntu-latest     steps:       - uses: actions/checkout@v3       - name: Setup Node         uses: actions/setup-node@v3         with:           node-version: '18'       - run: npm install       - run: npm test`

---

### 12.5 Releases & Pages

- **Releases**: formalized snapshots (often tied to tags).
- **Pages**: host static websites from a repo branch.

---

## 13\. Collaboration Workflows

Pick a workflow that suits your project size and team. Below are common ones.

---

### 13.1 Feature Branch Workflow (simple & common)

- Create a branch per feature:

  `git checkout -b feature/awesome`

- Work & commit locally
- Push branch and open PR
- After review, merge into `main` and delete branch

Advantages: clear isolation, easy code reviews.

---

### 13.2 Fork & Pull Request Workflow (open-source)

- Fork upstream repo
- Clone fork locally
- Create feature branch, push to fork
- Open PR from fork/feature to upstream/main

Advantage: contributors don’t need direct push access to upstream.

---

### 13.3 Gitflow Workflow (more formal)

Branches:

- `main` (production)
- `develop` (integration)
- `feature/*`, `release/*`, `hotfix/*`

Commands are more formalized (tools like `git-flow` help). Suitable for release-managed projects.

---

### 13.4 Trunk-Based Development

Short-lived feature branches (or direct commits) merged into main frequently. Prefer small incremental changes and feature toggles.

---

### 13.5 Choosing a workflow

Consider:

- Team size
- Release cadence
- CI/CD maturity
- Code review expectations

Document the chosen workflow in repo README to align the team.

---

## 14\. Rebasing (Explained Simply)

Rebasing takes a set of commits and moves them to a new base. It rewrites history to produce a linear commit sequence.

---

### 14.1 Why rebase?

- Keep history linear and tidy.
- Apply your feature commits on top of the latest `main` before merging.

---

### 14.2 Example

Current state:

`A - B - C (main)      \       D - E (feature)`

Rebasing the feature onto `main`:

`git checkout feature git rebase main`

Result:

`A - B - C - D' - E' (feature)`

Now the feature branch looks as if it was developed after `C`, which can simplify history.

---

### 14.3 Rebase vs Merge

- `merge` preserves branch history, creates merge commits.
- `rebase` rewrites commits to appear on top of another branch (no merge commit for the integration).

**Important:** Do not rebase commits that have already been pushed and shared with others unless everyone agrees — rebasing rewrites history and will force collaborators to reconcile.

---

### 14.4 Interactive rebase (preview)

`git rebase -i main`

This allows you to reorder, squash, edit, or drop commits (more on this in section 15).

---

### 14.5 Handling rebase conflicts

Conflicts during rebase are handled commit-by-commit:

1.  Fix conflicts in files
2.  `git add <file>`
3.  `git rebase --continue`

To abort a rebase:

`git rebase --abort`

---

## 15\. Interactive Rebase (History Cleanup)

Interactive rebase (`git rebase -i`) is a powerful tool to rewrite a sequence of commits. Use it to clean up commit messages, squash tiny commits, or reorder logical steps.

---

### 15.1 Common actions in interactive rebase

- `pick` — use commit
- `reword` — change commit message
- `edit` — pause to amend the commit
- `squash` — combine this commit into previous (keep both messages)
- `fixup` — combine into previous and discard this commit's message
- `drop` — remove the commit

Run it:

`git rebase -i HEAD~4 # opens an editor with the last 4 commits listed`

---

### 15.2 Example: Squash multiple commits into one

Editor shows:

`pick a1b2c3 Add basic structure pick d4e5f6 Add helper functions pick 7g8h9i Fix bug in helper`

Change to:

`pick a1b2c3 Add basic structure squash d4e5f6 Add helper functions squash 7g8h9i Fix bug in helper`

Save and exit. Git will combine all three into one commit and prompt to edit the combined commit message.

---

### 15.3 Reword a commit message

Change `pick` to `reword` (or `r`) for the commit you want to change.

---

### 15.4 Edit a commit

Change `pick` to `edit`. Rebase pauses at that commit:

`# make changes git add modified-files git commit --amend git rebase --continue`

---

### 15.5 Safety tips

- Don’t rebase public/shared commits without coordination.
- Use `git reflog` to recover if something goes wrong.
- Consider creating a backup branch before large rebase: `git branch backup-feature`.

---

## 16\. Git Tags

Tags mark important points in history — often used for releases.

---

### 16.1 Two kinds of tags

- **Lightweight tag** — like a bookmark to a commit:

  `git tag v1.0.0`

- **Annotated tag** — stored as full objects, include message, tagger, date:

  `git tag -a v1.0.0 -m "Release 1.0.0"`

Annotated tags are recommended for releases.

---

### 16.2 Listing and viewing tags

- List tags:

  `git tag`

- Show tag details:

  `git show v1.0.0`

---

### 16.3 Pushing tags to remote

- Push a single tag:

  `git push origin v1.0.0`

- Push all tags:

  `git push --tags`

---

### 16.4 Checking out a tag

`git checkout v1.0.0` puts you in a detached HEAD. Create a branch if you want to make changes:

`git checkout -b hotfix v1.0.0`

---

### 16.5 Deleting tags

- Delete local tag:

  `git tag -d v1.0.0`

- Delete remote tag:

  `git push origin :refs/tags/v1.0.0 # or git push origin --delete tag v1.0.0`

---
