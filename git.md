# git vs Github 

## Git 

* ### A local version control system software installed on your computer. It tracks changes to files, keeps a history of your work, and allows offline collaboration

## Github 

* ### A cloud-based platform that hosts Git repositories online. It acts as a centralized server so teams can share, back up, and collaborate on their Git projects easily.

## Git concepts 

### 1. Repository (Repo): The project folder where Git stores all your files and the complete history of every change made to them.

### 2.Local Repo: The copy of the repository that lives directly on your computer.

### 3. Remote Repo: The copy of the repository hosted online (e.g., on GitHub) for backing up or sharing with others.

### 4. Commit: A saved "snapshot" of your project at a specific point in time. Each commit acts as a restore point in your project's history.

### 5. Branch: An isolated timeline or workspace within your project. It lets you experiment, fix bugs, or build new features without changing the stable "main" code.

### 6. Merge: The process of combining changes from one branch into another (e.g., pulling a completed feature branch back into the main branch)

# Generating SSH Keys & GitHub Settings

### Create a pair of ssh keys 

```bash
ssh-keygen -t ecdsa
```
### Display the contents 

```bash
cat ~/.ssh/id_ecdsa.pub
```
## Key Pairs 

### 1. Private Key (id_ecdsa): Stored safely on your computer. Never share it.

### 2. Public Key (id_ecdsa.pub): Uploaded to GitHub settings. Acts as the lock your private key opens.



# Questions in Git module 


# Module: Introduction to Git, GitHub, and SSH Authentication

This module introduces **Git**, **GitHub**, and core version control workflows. Software development teams use these tools to store, share, edit, and manage code in a distributed manner. 

>  **Note:** You do not need to be a software developer to use Git. It is highly effective for creating documentation and managing informational files. For example, Quatrix mentors use a GitHub repository to document all their answers for the mentorship program.

---

##  1. Git vs. GitHub: Understanding the Difference

These two terms are often interchanged, but they refer to completely different parts of the workflow:

*   **Git:** A local **version control system** software. You install it on your computer (or office server) to track file history and manage repositories locally or across a private distributed network.
*   **GitHub (GitLab, Bitbucket, etc.):** Cloud-based companies that provide **hosted Git servers**. Instead of building and maintaining your own server infrastructure, you use their platform to collaborate and back up files.

### Pros & Cons of Cloud Hosting (GitHub/GitLab):
*   **Pros:** Less headache. You do not have to set up, maintain, or upgrade a physical Git server.
*   **Cons:** These are third-party services. They may require paid tiers for advanced features, and you must trust them to securely protect your data.

---

##  2. SSH Keys & Authentication Settings

To interact with remote repositories safely, it is highly recommended to use the **SSH protocol** instead of **HTTPS**.

### Why SSH?
*   **SSH:** Uses a secure, digital key pair generated on your PC. Once set up, authentication happens seamlessly in the background without prompting you for credentials.
*   **HTTPS:** Requires entering your username and a Personal Access Token (PAT) regularly, making password management tedious.

### How SSH Key Pairs Work
An SSH key pair consists of two interconnected cryptographic files:
1.  **Private Key (`id_ecdsa`):** Stored securely on your local computer. **Never share this file or expose its contents.**
2.  **Public Key (`id_ecdsa.pub`):** Stored on your GitHub account. It acts as a digital lock that only your specific private key can open.

>  **Important:** SSH keys are tied to physical hardware. If you use multiple computers (e.g., one at home and one at the office), you must generate a unique key pair on **each PC** and add both public keys to your GitHub account settings. You can also re-use these generated keys to gain access to remote Linux servers managed by network administrators.

### Step-by-Step: Generating & Adding SSH Keys
1. Open a terminal or shell session.
2. Run the generation command:
   ```bash
   ssh-keygen -t ecdsa
   ```
3. Press **Enter** to accept the default file storage location.
4. View your newly generated public key:
   ```bash
   cat ~/.ssh/id_ecdsa.pub
   ```
5. Copy the entire output string (which will look similar to `ssh-ecdsa AAAAB3Nza... user@home-pc`).
6. Navigate to your personal **GitHub Account Settings** ➡️ **SSH and GPG keys**.
7. Click **New SSH key**, give it a descriptive title (e.g., "Work Laptop"), paste the text into the **Key** field, and click **Add SSH key**.

---

## 3. Git Branches & Workflow Core Concepts

A Git repository records the chronological evolution of your project folder using timelines called **Branches**. 

### The Pristine Main Branch
*   Every repository has a default base timeline, usually named `main` (or `master` in older setups). 
*   In team projects, the `main` branch is typically **protected**. You cannot push code directly to it. Changes must go through a **Pull Request (or Merge Request)** to be reviewed and approved by teammates first.

### What is a Commit?
*   A **Commit** is a saved snapshot of your project's state. 
*   Every commit must include a meaningful message describing what was accomplished. 
*   Commits act as historical restore points, allowing you to easily roll your codebase back if you go astray.

### Sandboxing with Branches
If your project ideas become complicated, or if you are collaborating with a team, you should create a secondary branch instead of working on the stable `main` timeline. 
*   Think of a branch as an isolated **sandbox** where you can safely test sub-ideas, experiment, or fix bugs.
*   Working in a separate branch keeps the core project stable and prevents you from introducing half-baked, breaking changes to your team.
*   **Merging:** Once your experimental feature is fully vetted and stable, you perform a merge to move your sandbox data back into the pristine `main` branch.

---

## 💻 4. Command Reference Guide

All Git operations are executed in your terminal by preceding them with the keyword `git`.

### `git help`
Provides the official manual documentation for any Git command.
```bash
git help clone
```

### `git config`
Configures settings tied to your global Git profile, such as your default text editor and author identity metadata.
```bash
git config --global core.editor "vim"
git config --global user.name "Paul Omollo"
git config --global user.email paul.omollo@quatrixglobal.com
```

### `git clone <URL>`
Downloads an exact copy of a remote repository (from platforms like GitHub) onto your local machine.
```bash
git clone git@github.com:quatrix-education/mentor.git
```
*To get a URL from GitHub: Open the repo landing page, click the green **"<> Code"** button, select the **SSH** tab, and copy the string.*

### `git checkout`
Switches between existing timelines or creates new branches out of your current working directory.
```bash
# Switch to an existing feature branch:
git checkout feature/add-bash-details

# Create (-b) and immediately switch to a new branch:
git checkout -b hotfix/correct-vi-details
```

### `git status`
Displays the real-time status of your working tree. It breaks files down into two states:
*   **Changes to be committed (Staged):** Modified files that have been successfully indexed and packaged, ready to be saved in the next commit.
*   **Changes not staged:** Modified files that Git detects, but will leave out of the next commit unless they are explicitly staged.

### `git diff`
Displays the exact, line-by-line file modifications made in your working directory that have not yet been staged.
```bash
git diff
```

```markdown
# Git & GitHub Complete Notes — Commands, Concepts, Workflows, Practice & Exam Questions

> A full compilation of Git and GitHub topics, commands, flags, workflows, practice questions, and exam-style answers.
> Copy this entire file into VS Code or GitHub as your study notes.

---

## Table of Contents

1. [What is Git?](#1-what-is-git)
2. [Git vs GitHub](#2-git-vs-github)
3. [Version Control Systems](#3-version-control-systems)
4. [Git Architecture — The Three Trees](#4-git-architecture--the-three-trees)
5. [Git Configuration](#5-git-configuration)
6. [Creating a Repository](#6-creating-a-repository)
7. [Basic Workflow — Add, Commit, Status](#7-basic-workflow--add-commit-status)
8. [Viewing Changes — diff and log](#8-viewing-changes--diff-and-log)
9. [Branching](#9-branching)
10. [Merging & Merge Conflicts](#10-merging--merge-conflicts)
11. [Remote Repositories & GitHub](#11-remote-repositories--github)
12. [Pushing, Pulling, and Fetching](#12-pushing-pulling-and-fetching)
13. [Undoing Changes](#13-undoing-changes)
14. [Stashing & Tagging](#14-stashing--tagging)
15. [Rebasing](#15-rebasing)
16. [.gitignore](#16-gitignore)
17. [GitHub Workflows](#17-github-workflows)
18. [Complete Command Reference (All Commands + Flags)](#18-complete-command-reference-all-commands--flags)
19. [Multiple Ways to Get the Same Output](#19-multiple-ways-to-get-the-same-output)
20. [Fill-in-the-Blank Rules](#20-fill-in-the-blank-rules)
21. [Practice Questions & Answers](#21-practice-questions--answers)
22. [Exam-Style Questions](#22-exam-style-questions)
23. [Quick Reference Cheat Sheet](#23-quick-reference-cheat-sheet)

---

## 1. What is Git?

**Git** is a free, open-source, **distributed version control system (DVCS)** created by **Linus Torvalds** in 2005 for managing the Linux kernel source code. It is primarily written in **C**.

**Key points:**
- Git is **distributed** — every developer has a full copy of the repository with its complete history.
- It tracks changes to files over time, allowing you to revert, compare, and collaborate.
- It is fast, portable, and secure.
- It works **locally** — you can commit without a network connection.
- **Git is not GitHub.** Git is the tool; GitHub is a hosting platform.

**Q: Who created Git and when?**
Linus Torvalds, 2005.

**Q: What does "distributed" mean?**
Every clone is a full repository with complete history — no single central server is required.

**Q: What is a repository (repo)?**
A directory tracked by Git, containing all files and the complete history of changes.

---

## 2. Git vs GitHub

| Git | GitHub |
|-----|--------|
| Distributed version control system | Hosting platform for Git repositories |
| Runs locally | Runs in the cloud |
| Works offline | Requires network |
| No account needed | Requires a GitHub account |
| Command-line tool | Web-based + CLI |
| Free and open source | Free tier + paid plans |

**Q: What is the difference between Git and GitHub?**
**Answer:** Git is the distributed version control system; GitHub is a hosting platform that adds collaboration features (pull requests, issues, Actions) on top of it.

---

## 3. Version Control Systems

| Type | Description | Examples |
|------|-------------|----------|
| Individual / File-Based | Manages single files, revisions are differentials | RCS |
| Centralized | One central server, clients check out/check in | CVS, SVN, Perforce |
| Distributed | Every copy is a full repository | Git, Mercurial, BitKeeper |

**Q: What are the three types of version control?**
Individual/File-Based, Centralized, and Distributed.

**Q: Why is distributed version control better than centralized?**
You can work offline, commit locally, and don't depend on a single server being available.

---

## 4. Git Architecture — The Three Trees

Git has three main areas:

| Area | Also Called | Description |
|------|-------------|-------------|
| Working Directory | Working tree | Where you edit files |
| Staging Area | Index | Where changes are prepared for commit |
| Repository | HEAD / .git | Where committed snapshots live |

**Flow:**
```
Working Directory  →  git add  →  Staging Area  →  git commit  →  Repository
```

**Q: What is the staging area (index)?**
A binary file that contains timestamps, checksums, and filenames — it holds changes ready for the next commit.

**Q: What is HEAD?**
A reference to the most recent commit in the currently checked-out branch.

---

## 5. Git Configuration

Git will complain if you don't have a name and email configured.

### Setting identity
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global color.ui auto
```

### Config scopes

| Scope | Location | Applies to |
|-------|----------|------------|
| `--global` | `~/.gitconfig` | All repos for your user |
| `--local` | `.git/config` | Current repo only |
| `--system` | `/etc/gitconfig` | All users on the machine |

### Viewing config
```bash
git config --list
git config user.name
```

### Other useful configs
```bash
git config --global core.editor "vim"
git config --global init.defaultBranch main
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.st status
```

**Q: What is the difference between `--global` and `--local`?**
`--global` applies to all repos for your user; `--local` applies only to the current repo.

---

## 6. Creating a Repository

### Initialize a new repo
```bash
git init
git init myproject
```
Creates a new empty repository in the current folder (or in `myproject`). This creates a `.git` subdirectory.

### Clone an existing repo
```bash
git clone https://github.com/user/repo.git
git clone https://github.com/user/repo.git myfolder
git clone -b branch-name https://github.com/user/repo.git
```
Downloads a project with the entire history from the remote repository.

**Q: What does `git init` do?**
Creates a new empty Git repository in the current directory (creates `.git/`).

**Q: What does `git clone` do?**
Downloads a project with its entire history from a remote repository.

---

## 7. Basic Workflow — Add, Commit, Status

### Check status
```bash
git status
git status -s              # Short format
git status --ignored       # Include ignored files
```
Displays the status of your working directory — new, staged, and modified files.

### Stage files
```bash
git add file.txt           # Stage one file
git add .                  # Stage all changes in current directory
git add *.txt              # Stage all .txt files
git add -A                 # Stage all changes (including deletions)
git add -p                 # Stage interactively (patch mode)
```

### Commit
```bash
git commit -m "Add login feature"
git commit -am "Fix bug"          # Stage tracked files + commit
git commit --amend                # Modify last commit
git commit --amend --no-edit      # Amend without changing message
```

**Q: What does `git add` do?**
Stages one or more files for the next commit.

**Q: What does `git commit` do?**
Creates a new commit from staged changes with a message.

**Q: What does `git status` show?**
Branch name, current commit, staged files, modified files, and untracked files.

---

## 8. Viewing Changes — diff and log

### Diff
```bash
git diff                    # Working dir vs staging area
git diff --staged           # Staging area vs last commit
git diff HEAD~1             # Working dir vs previous commit
git diff branch1..branch2   # Between two branches
```

### Log
```bash
git log                     # Full commit history
git log --oneline           # Compact, one line per commit
git log --graph --decorate  # Visual graph with refs
git log -n 5                # Last 5 commits
git log -p                  # Show patch details
git log --author="John"     # Filter by author
git log --since="1 week ago"  # Since date
```

**Q: What does `git log --oneline` do?**
Shows a compact commit history — one commit per line.

**Q: How do you see changes between staged and committed?**
`git diff --staged` or `git diff --cached`.

---

## 9. Branching

A **branch** is a lightweight movable pointer to a commit.

### Create and switch
```bash
git branch feature            # Create branch (stay on current)
git checkout -b feature       # Create AND switch
git switch -c feature         # Modern alternative
git checkout feature          # Switch to branch
git switch feature            # Modern switch
```

### List branches
```bash
git branch                    # Local branches
git branch -a                 # All branches (local + remote)
git branch -r                 # Remote branches only
git branch -v                 # With last commit
```

### Delete branches
```bash
git branch -d feature         # Delete (must be merged)
git branch -D feature         # Force delete
git push origin --delete feature  # Delete remote branch
```

### Rename branch
```bash
git branch -m oldname newname
git branch -m newname         # Rename current branch
```

**Q: How do you create a new branch and switch to it immediately?**
```bash
git checkout -b newbranch
# or
git switch -c newbranch
```

**Q: What is a branch?**
A lightweight movable pointer to a commit — enables parallel development.

---

## 10. Merging & Merge Conflicts

Combine changes from one branch into another.

### Merge workflow
```bash
git checkout main             # Go to target branch
git merge feature             # Merge feature into main
git merge --no-ff feature     # Merge with a merge commit
git merge --abort             # Abort a conflicted merge
```

### Conflict markers
```
<<<<<<< HEAD
She plays a lot.
=======
She loves to sleep.
>>>>>>> cats
```
- `<<<<<<< HEAD` → your current branch's version
- `=======` → separator
- `>>>>>>> cats` → incoming branch's version

### Resolving conflicts
1. Open the conflicted file(s)
2. Edit to keep the desired version
3. Stage the resolved files: `git add .`
4. Continue the merge: `git merge --continue` or abort: `git merge --abort`

**Q: What is a merge conflict?**
Occurs when Git cannot automatically merge changes because both branches modified the same part of a file.

**Q: How do you resolve a merge conflict?**
Edit the file, remove conflict markers, choose the correct content, then `git add` and `git commit` (or `git merge --continue`).

---

## 11. Remote Repositories & GitHub

A **remote** is a repository hosted elsewhere (GitHub, GitLab, Bitbucket).

### Managing remotes
```bash
git remote -v                                     # List remotes
git remote add origin https://github.com/user/repo.git  # Add remote
git remote remove origin                          # Remove remote
git remote rename old new                         # Rename
git remote set-url origin new-url                 # Change URL
```

**Q: What is a remote?**
A repository hosted on a server (GitHub, GitLab) that you sync with.

**Q: What does `origin` mean?**
The default name for the remote repository you cloned from.

---

## 12. Pushing, Pulling, and Fetching

### Push
```bash
git push origin main              # Push to main
git push -u origin main           # Set upstream + push
git push                          # Push (if upstream set)
git push --tags                   # Push tags
git push --force-with-lease       # Safer force push
```

### Pull
```bash
git pull origin main              # Fetch + merge
git pull                          # Pull (if upstream set)
git pull --rebase                 # Pull with rebase
```

### Fetch vs Pull

| `git fetch` | `git pull` |
|-------------|------------|
| Downloads changes only | Downloads + merges |
| Does not modify working dir | Modifies working dir |
| Safe — review before merge | Automatic merge |

```bash
git fetch origin
git log HEAD..origin/main         # See what's new
git merge origin/main             # Merge manually
```

**Q: What does `git push` do?**
Uploads local commits to a remote repository.

**Q: What does `git pull` do?**
Fetches changes from remote and merges them into your current branch.

**Q: What is the difference between `git fetch` and `git pull`?**
`git fetch` downloads changes without merging; `git pull` downloads and merges in one step.

---

## 13. Undoing Changes

### Discard working directory changes
```bash
git checkout -- file.txt          # Discard changes in file
git restore file.txt              # Modern alternative
git restore .                     # Discard all changes
```

### Unstage files
```bash
git reset HEAD file.txt           # Unstage file
git restore --staged file.txt     # Modern alternative
```

### Undo last commit
```bash
git reset --soft HEAD~1           # Undo commit, keep staged
git reset --mixed HEAD~1          # Undo commit, keep working (default)
git reset --hard HEAD~1           # Undo commit, discard changes (DANGEROUS)
```

### Revert a commit (safe)
```bash
git revert abc1234                # Creates a new commit that undoes abc1234
```

### Remove files
```bash
git rm file.txt                   # Remove from working dir + index
git rm --cached file.txt          # Remove from index only (keep file)
git clean -f                      # Delete untracked files
git clean -fd                     # Delete untracked files + directories
```

**Q: Difference between `git reset` and `git revert`?**
`git reset` removes commits from history; `git revert` creates a new commit that undoes changes. `revert` is safe for shared branches; `reset` is not.

**Q: What does `git reset --hard HEAD~1` do?**
Removes the last commit and discards all changes.

---

## 14. Stashing & Tagging

### Stashing
**Stash** saves uncommitted changes temporarily.

```bash
git stash                         # Stash changes
git stash save "work in progress" # Stash with message
git stash list                    # List stashes
git stash pop                     # Apply + remove from stash
git stash apply                   # Apply (keep in stash)
git stash drop                    # Delete a stash
git stash clear                   # Delete all stashes
```

### Tagging
**Tags** mark specific commits (releases, versions).

```bash
git tag                           # List tags
git tag v1.0.0                    # Lightweight tag
git tag -a v1.0.0 -m "Release"   # Annotated tag
git tag -d v1.0.0                 # Delete local tag
git push origin v1.0.0            # Push specific tag
git push --tags                   # Push all tags
```

| Type | Description |
|------|-------------|
| Lightweight | Just a pointer to a commit |
| Annotated | Full object with tagger, date, message |

**Q: Difference between `git stash pop` and `git stash apply`?**
`pop` applies and removes the stash; `apply` applies but keeps it.

**Q: Difference between lightweight and annotated tags?**
Lightweight is just a pointer; annotated includes tagger info, date, and message.

---

## 15. Rebasing

**Rebase** moves or combines commits onto a new base, creating a linear history.

```bash
git rebase main                   # Rebase current branch onto main
git rebase -i HEAD~3              # Interactive rebase (last 3 commits)
git rebase --continue             # After resolving conflicts
git rebase --abort                # Abort rebase
```

Interactive rebase actions: `pick`, `reword`, `edit`, `squash`, `fixup`, `drop`.

**Q: When should you NOT rebase?**
On shared/public branches — it rewrites history and can cause problems for others.

**Q: What is the difference between merge and rebase?**
Merge preserves history and creates a merge commit; rebase creates a linear history by rewriting commits.

---

## 16. .gitignore

A `.gitignore` file tells Git which files/directories to ignore.

```
# Ignore build output
build/
dist/
*.o
*.exe

# Ignore logs
*.log
logs/

# Ignore environment files
.env
venv/
node_modules/

# Ignore OS files
.DS_Store
Thumbs.db
```

**Q: What does `.gitignore` do?**
Tells Git not to track specified files, such as build output and local configuration.

**Q: Does `.gitignore` affect already tracked files?**
No. It only affects untracked files. You must `git rm --cached` to stop tracking a file that's already committed.

---

## 17. GitHub Workflows

### Feature Branch Workflow
1. Create a branch for each feature
2. Commit changes to the branch
3. Push branch to remote
4. Open a Pull Request
5. Review and merge into main

```bash
git checkout -b feature/login
# make changes
git add .
git commit -m "Add login"
git push -u origin feature/login
# open PR on GitHub
```

### Fork and Pull Workflow (open source)
1. Fork the repository on GitHub
2. Clone your fork
3. Create a feature branch
4. Commit and push to your fork
5. Open a Pull Request to the upstream repo

### Git Flow
- `main` — production
- `develop` — integration
- `feature/*` — features
- `release/*` — release prep
- `hotfix/*` — urgent fixes

**Q: What is the recommended way to propose a change for review?**
Create a branch, push it, and open a pull request.

**Q: How does an outside contributor propose changes?**
Fork the repository, commit to a branch in their fork, and open a pull request to the upstream repository.

---

## 18. Complete Command Reference (All Commands + Flags)

### Setup and Configuration
| Command | Purpose |
|---------|---------|
| `git config --global user.name "Name"` | Set name |
| `git config --global user.email "email"` | Set email |
| `git config --list` | List config |
| `git config --global alias.co checkout` | Create alias |

### Getting and Creating Projects
| Command | Purpose |
|---------|---------|
| `git init` | Create new repo |
| `git clone url` | Clone repo |

### Basic Snapshotting
| Command | Purpose |
|---------|---------|
| `git status` | Show status |
| `git add file` | Stage file |
| `git add .` | Stage all |
| `git commit -m "msg"` | Commit |
| `git commit -am "msg"` | Stage tracked + commit |
| `git commit --amend` | Amend last commit |
| `git diff` | Working vs staging |
| `git diff --staged` | Staging vs committed |
| `git rm file` | Remove file |
| `git rm --cached file` | Untrack file |

### Branching and Merging
| Command | Purpose |
|---------|---------|
| `git branch` | List branches |
| `git branch -a` | All branches |
| `git branch name` | Create branch |
| `git checkout name` | Switch branch |
| `git checkout -b name` | Create + switch |
| `git switch -c name` | Create + switch (modern) |
| `git branch -d name` | Delete merged branch |
| `git branch -D name` | Force delete |
| `git merge name` | Merge branch |
| `git merge --abort` | Abort merge |
| `git rebase name` | Rebase onto branch |
| `git rebase -i HEAD~n` | Interactive rebase |
| `git cherry-pick hash` | Apply specific commit |

### Sharing and Updating
| Command | Purpose |
|---------|---------|
| `git remote -v` | List remotes |
| `git remote add origin url` | Add remote |
| `git fetch origin` | Download changes |
| `git pull origin main` | Fetch + merge |
| `git push origin main` | Push |
| `git push -u origin main` | Set upstream + push |
| `git push --tags` | Push tags |

### Inspection
| Command | Purpose |
|---------|---------|
| `git log` | Commit history |
| `git log --oneline` | Compact log |
| `git log --graph --decorate` | Visual graph |
| `git show hash` | Show commit |
| `git blame file` | Who changed each line |
| `git reflog` | Reference log |

### Undoing
| Command | Purpose |
|---------|---------|
| `git checkout -- file` | Discard changes |
| `git restore file` | Discard changes (modern) |
| `git reset HEAD file` | Unstage |
| `git restore --staged file` | Unstage (modern) |
| `git reset --soft HEAD~1` | Undo commit, keep staged |
| `git reset --hard HEAD~1` | Undo commit, discard all |
| `git revert hash` | Revert commit (safe) |

### Stashing and Tagging
| Command | Purpose |
|---------|---------|
| `git stash` | Stash changes |
| `git stash pop` | Apply + remove |
| `git stash apply` | Apply, keep stash |
| `git tag v1.0` | Lightweight tag |
| `git tag -a v1.0 -m "msg"` | Annotated tag |

---

## 19. Multiple Ways to Get the Same Output

### 19.1 Create a new branch and switch
```bash
git checkout -b feature
git switch -c feature
git branch feature && git checkout feature
```

### 19.2 Stage all changes
```bash
git add .
git add -A
git add --all
```

### 19.3 Commit all tracked changes
```bash
git commit -am "message"
git add -u && git commit -m "message"
```

### 19.4 Discard working directory changes
```bash
git checkout -- file.txt
git restore file.txt
```

### 19.5 Unstage a file
```bash
git reset HEAD file.txt
git restore --staged file.txt
```

### 19.6 View compact log
```bash
git log --oneline
git log --pretty=oneline
git log --format="%h %s"
```

### 19.7 Undo last commit (keep changes)
```bash
git reset --soft HEAD~1
git reset --soft HEAD^
```

### 19.8 Get the current branch name
```bash
git branch --show-current
git rev-parse --abbrev-ref HEAD
```

---

## 20. Fill-in-the-Blank Rules

When the question shows part of the command, only write the missing part:

| Question | Answer | NOT |
|----------|--------|-----|
| `git ___ -m "msg"` (save changes) | `commit` | `git commit` |
| `git ___ -b feature` (create + switch) | `checkout` | `git checkout` |
| `git ___ origin main` (upload) | `push` | `git push` |
| `git ___ --oneline` (compact log) | `log` | `git log` |
| `git ___ --staged` (show staged changes) | `diff` | `git diff` |
| `git ___ HEAD~1` (undo commit) | `reset` | `git reset` |
| `git ___ .` (stage all) | `add` | `git add` |
| `git ___ -a v1.0 -m "Release"` (tag) | `tag` | `git tag` |
| `git ___ origin` (download changes) | `fetch` | `git fetch` |

---

## 21. Practice Questions & Answers

### Section A: Git Basics
**Q1.** What is Git?
**Answer:** A distributed version control system for tracking changes in source code.

**Q2.** Who created Git and when?
**Answer:** Linus Torvalds, 2005.

**Q3.** Difference between Git and GitHub?
**Answer:** Git is the DVCS; GitHub is a hosting platform for Git repos.

**Q4.** What are the three areas of Git?
**Answer:** Working directory, staging area (index), and repository.

**Q5.** What does `git init` do?
**Answer:** Creates a new empty Git repository (`.git/` directory).

### Section B: Basic Workflow
**Q6.** How do you stage a file?
**Answer:** `git add file.txt`

**Q7.** How do you commit with a message?
**Answer:** `git commit -m "message"`

**Q8.** What does `git status` show?
**Answer:** Branch name, current commit, staged files, modified files, untracked files.

### Section C: Branching
**Q9.** How do you create a branch and switch to it?
**Answer:** `git checkout -b feature` or `git switch -c feature`.

**Q10.** How do you merge a branch?
**Answer:** `git checkout main && git merge feature`

**Q11.** How do you delete a branch?
**Answer:** `git branch -d feature` (merged) or `git branch -D feature` (force).

### Section D: Remote Repositories
**Q12.** How do you add a remote?
**Answer:** `git remote add origin https://github.com/user/repo.git`

**Q13.** Difference between `git fetch` and `git pull`?
**Answer:** `fetch` downloads only; `pull` downloads and merges.

**Q14.** How do you push to a remote?
**Answer:** `git push -u origin main`

### Section E: Undoing Changes
**Q15.** How do you unstage a file?
**Answer:** `git reset HEAD file.txt` or `git restore --staged file.txt`

**Q16.** Difference between `git reset` and `git revert`?
**Answer:** `reset` rewrites history; `revert` creates a new undo commit.

### Section F: Conflicts & Stashing
**Q17.** What causes a merge conflict?
**Answer:** Both branches modified the same part of a file.

**Q18.** What does `git stash` do?
**Answer:** Temporarily saves uncommitted changes.

---

## 22. Exam-Style Questions

**Q1.** What is the difference between Git and GitHub?
a) They are the same
b) Git is the DVCS; GitHub is a hosting platform that adds collaboration features
c) GitHub replaces Git
d) Git only works with GitHub

**Answer: b**

---

**Q2.** A change should be proposed for review before it enters `main`. What do you do?
a) Commit directly to `main`
b) Create a branch, push it, and open a pull request
c) Email a patch
d) Fork and never merge

**Answer: b**

---

**Q3.** A contributor outside the organization wants to propose a change to a public repository. What do they do?
a) They need write access
b) Fork the repository, commit to a branch in their fork, and open a pull request to the upstream repository
c) They cannot contribute
d) Clone and push directly

**Answer: b**

---

**Q4.** What does a `.gitignore` file do?
a) Deletes files
b) Tells Git not to track specified files
c) Hides files from other users
d) Encrypts files

**Answer: b**

---

**Q5.** A pull request description contains `Closes #42`. What happens?
a) Nothing
b) Issue 42 is automatically closed when the PR merges
c) The issue is deleted
d) The issue is assigned

**Answer: b**

---

**Q6.** Which command stages changes for the next commit?
a) `git commit`
b) `git add`
c) `git push`
d) `git status`

**Answer: b**

---

**Q7.** What command creates a new branch and switches to it immediately?
a) `git branch newbranch`
b) `git checkout -b newbranch`
c) `git merge newbranch`
d) `git switch newbranch`

**Answer: b**

---

**Q8.** How many ways are present in Git to integrate changes from one branch into another?
a) 3
b) 5
c) 2
d) 4

**Answer: c** (merge and rebase)

---

**Q9.** What does `git revert c87e6ae4` do?
a) Has no effect
b) Creates a new commit that undoes the changes from commit c87e6ae4
c) Deletes the commit
d) Resets to that commit

**Answer: b**

---

**Q10.** In the command `git gc`, what does `gc` stand for?
a) Git commit
b) Garbage collection
c) Get changes
d) Global config

**Answer: b**

---

**Q11.** What does `git blame some_file` do?
a) Deletes the file
b) Shows who last modified each line and when
c) Ignores the file
d) Renames the file

**Answer: b**

---

**Q12.** What is the difference between `git pull` and `git fetch`?
**Answer:** `git fetch` downloads changes from remote but does not merge them; `git pull` downloads and merges in one step.

---

**Q13.** What is a merge conflict and how do you resolve it?
**Answer:** A merge conflict occurs when both branches modify the same part of a file. Git inserts conflict markers. Edit the file, choose the correct content, remove markers, then `git add` and `git commit`.

---

**Q14.** What are the key states in Git?
**Answer:** Working Directory → Staging Area → Repository (committed).

---

**Q15.** What is a branch?
**Answer:** A lightweight movable pointer to a commit.

---

**Q16.** What is a commit in Git?
**Answer:** A snapshot of changes with a message, author, and timestamp.

---

**Q17.** What is `git merge`?
**Answer:** Combines changes from one branch into another.

---

**Q18.** What is `git rebase`?
**Answer:** Moves or combines commits onto a new base, creating linear history.

---

**Q19.** What is `git stash`?
**Answer:** Temporarily saves uncommitted changes so you can work on something else.

---

**Q20.** What is a tag in Git?
**Answer:** A marker for a specific commit (e.g., release version).

---

## 23. Quick Reference Cheat Sheet

| Task | Command |
|------|---------|
| Configure name | `git config --global user.name "Name"` |
| Configure email | `git config --global user.email "email"` |
| Create repo | `git init` |
| Clone repo | `git clone url` |
| Check status | `git status` |
| Stage file | `git add file` |
| Stage all | `git add .` |
| Commit | `git commit -m "msg"` |
| Stage + commit | `git commit -am "msg"` |
| View changes | `git diff` |
| View staged changes | `git diff --staged` |
| View log | `git log --oneline` |
| Visual log | `git log --graph --decorate` |
| Create branch | `git branch name` |
| Create + switch | `git checkout -b name` |
| Switch branch | `git checkout name` |
| List branches | `git branch -a` |
| Merge branch | `git merge name` |
| Abort merge | `git merge --abort` |
| Add remote | `git remote add origin url` |
| List remotes | `git remote -v` |
| Fetch changes | `git fetch origin` |
| Pull changes | `git pull origin main` |
| Push changes | `git push -u origin main` |
| Undo commit (keep) | `git reset --soft HEAD~1` |
| Undo commit (discard) | `git reset --hard HEAD~1` |
| Revert commit | `git revert hash` |
| Discard changes | `git checkout -- file` |
| Unstage | `git reset HEAD file` |
| Stash changes | `git stash` |
| Apply stash | `git stash pop` |
| List stashes | `git stash list` |
| Tag release | `git tag -a v1.0 -m "msg"` |
| Push tags | `git push --tags` |
| Interactive rebase | `git rebase -i HEAD~n` |
| Cherry-pick | `git cherry-pick hash` |
| Ignore file | Add to `.gitignore` |
| View current branch | `git branch --show-current` |
| View reflog | `git reflog` |
| Blame file | `git blame file` |
| Help | `git help command` |
| Git version | `git --version` |

```markdown
# Git & GitHub Complete Notes — Full Explanations

> A full compilation of Git and GitHub topics, commands, flags, workflows, practice questions, and exam-style answers — **with detailed explanations for every concept.**
> Copy this entire file into VS Code or GitHub as your study notes.

---

## Table of Contents

1. [What is Git?](#1-what-is-git)
2. [Git vs GitHub](#2-git-vs-github)
3. [Version Control Systems](#3-version-control-systems)
4. [Git Architecture — The Three Trees](#4-git-architecture--the-three-trees)
5. [Git Configuration](#5-git-configuration)
6. [Creating a Repository](#6-creating-a-repository)
7. [Basic Workflow — Add, Commit, Status](#7-basic-workflow--add-commit-status)
8. [Viewing Changes — diff and log](#8-viewing-changes--diff-and-log)
9. [Branching](#9-branching)
10. [Merging & Merge Conflicts](#10-merging--merge-conflicts)
11. [Remote Repositories & GitHub](#11-remote-repositories--github)
12. [Pushing, Pulling, and Fetching](#12-pushing-pulling-and-fetching)
13. [Undoing Changes](#13-undoing-changes)
14. [Stashing & Tagging](#14-stashing--tagging)
15. [Rebasing](#15-rebasing)
16. [.gitignore](#16-gitignore)
17. [GitHub Workflows](#17-github-workflows)
18. [Complete Command Reference (All Commands + Flags)](#18-complete-command-reference-all-commands--flags)
19. [Multiple Ways to Get the Same Output](#19-multiple-ways-to-get-the-same-output)
20. [Fill-in-the-Blank Rules](#20-fill-in-the-blank-rules)
21. [Practice Questions & Answers](#21-practice-questions--answers)
22. [Exam-Style Questions](#22-exam-style-questions)
23. [Quick Reference Cheat Sheet](#23-quick-reference-cheat-sheet)

---

## 1. What is Git?

**Git** is a free, open-source, **distributed version control system (DVCS)** created by **Linus Torvalds** in 2005 to manage the Linux kernel source code. It is primarily written in **C**.

### Detailed Explanation

Git was created because the Linux kernel developers needed a tool to manage thousands of contributors submitting code changes simultaneously. The previous tool (BitKeeper) was proprietary and the free license was revoked, so Linus built Git from scratch in about two weeks.

**Why Git is important:**

- **Version control:** Tracks every change made to a file, so you can see what changed, when, and by whom.
- **Collaboration:** Multiple developers can work on the same project without overwriting each other's work.
- **Backup/restore:** You can revert to any previous version of your project.
- **Branching:** You can experiment on separate branches without affecting the main code.
- **Offline work:** Because it's distributed, you can commit changes without internet.

**Key characteristics:**

- **Distributed:** Every developer has a full copy of the entire repository (including history). There's no single point of failure.
- **Fast:** Most Git operations are local, so they happen almost instantly.
- **Secure:** Every file and commit is checksummed (SHA-1 hash) before storage.
- **Open source:** Free to use, modify, and distribute.

**Q: Who created Git and when?**
**A:** Linus Torvalds, in 2005, to manage the Linux kernel source code.

**Q: What does "distributed" mean?**
**A:** Every person who clones a repository gets a full copy — including all commits, branches, and history. No single central server is required for most operations.

**Q: What is a repository (repo)?**
**A:** A directory tracked by Git, containing your project files and a hidden `.git` folder that stores the entire history of the project.

---

## 2. Git vs GitHub

### Detailed Explanation

Many beginners confuse Git and GitHub because they are often used together, but they are entirely different things:

| Feature | Git | GitHub |
|---------|-----|--------|
| What is it? | A version control tool | A web-based hosting service |
| Where does it run? | On your local machine | In the cloud (github.com) |
| Network required? | No — works offline | Yes — requires internet |
| Account needed? | No | Yes |
| Interface | Command line (mostly) | Web UI + CLI + Desktop app |
| Ownership | Open-source (GPL) | Owned by Microsoft |
| Purpose | Track changes | Host and share Git repos |
| Features | Commits, branches, merges | Pull requests, issues, Actions, wiki, code review |
| Alternatives | Mercurial, SVN, Perforce | GitLab, Bitbucket, Gitea |

**Think of it this way:** Git is like a **camera** (it captures snapshots of your work). GitHub is like **Instagram** (a platform where you upload and share those snapshots).

**Q: What is the difference between Git and GitHub?**
**A:** Git is the distributed version control system itself (a local tool). GitHub is a hosting platform that stores Git repositories online and adds collaborative features like pull requests, issues, and code review.

---

## 3. Version Control Systems

### Detailed Explanation

A **Version Control System (VCS)** is software that tracks changes to files over time so you can recall specific versions later. There are three generations:

### 1. Local / Individual VCS
- Example: RCS (Revision Control System)
- Only tracks one file at a time.
- Stores each version as a **differential** (only the changes).
- No collaboration — lives only on your machine.

### 2. Centralized VCS
- Examples: CVS, Subversion (SVN), Perforce
- One **central server** stores the repository.
- Developers **check out** files, make changes, and **check in**.
- **Downside:** If the server goes down, nobody can work. If the server's hard drive dies and there's no backup, you lose everything.

### 3. Distributed VCS
- Examples: Git, Mercurial, BitKeeper
- Every developer **clones** the entire repository (with full history) to their local machine.
- You can commit, branch, and view history **offline**.
- Syncing happens separately (`push` / `pull`).
- **Advantages:** Fast, resilient (any clone is a backup), flexible workflows.

**Q: What are the three types of version control?**
**A:** Local (Individual), Centralized, and Distributed.

**Q: Why is distributed version control better?**
**A:** It works offline, is faster (local operations), and no single server is a point of failure. Any clone can restore the project.

---

## 4. Git Architecture — The Three Trees

### Detailed Explanation

Git has **three main areas** where files exist as you work:

### 1. Working Directory (Working Tree)
This is your actual project folder — where you edit files with your editor. When you make changes, Git detects them here but does not yet track them for the next commit.

### 2. Staging Area (Index)
A middle layer between your working directory and the repository. When you run `git add`, files move here. This lets you **choose exactly which changes** go into the next commit — not necessarily all of them.

The staging area is a **binary file** that stores:
- Timestamps
- Checksums (SHA-1 hashes)
- Filenames and file paths
- References to file versions

### 3. Repository (HEAD / .git)
Once you run `git commit`, the staged changes are permanently saved in the `.git` folder as a **commit object**. `HEAD` is a special pointer that always points to the latest commit in your current branch.

### The Flow Diagram

```
+---------------------+    git add    +------------------+    git commit    +-----------------+
|  Working Directory  | -------------> |  Staging Area    | ---------------> |  Repository     |
|  (your files)       |                |  (index)         |                  |  (.git / HEAD)  |
+---------------------+                +------------------+                  +-----------------+
```

**Q: What is the staging area (index)?**
**A:** A binary file that contains timestamps, checksums, and filenames of staged files. It holds the changes that will be included in the next commit.

**Q: What is HEAD?**
**A:** A reference (pointer) to the most recent commit in the currently checked-out branch.

**Q: What is the working tree?**
**A:** The directory where you can access and edit all your project source files.

**Q: What is the correct order of the Git workflow?**
**A:** Edit files → `git add` (stage) → `git commit` (save to repository).

---

## 5. Git Configuration

### Detailed Explanation

Before you can commit, Git needs to know who you are. Otherwise, every commit is anonymous and can't be attributed to you. This is why Git will complain if you try to commit without a `user.name` and `user.email`.

### Setting Identity

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global color.ui auto
```

**What each line does:**
- `git config` → the command to manage Git configuration.
- `--global` → stores in `~/.gitconfig`, applies to **all repos on your machine** for your user.
- `user.name "Your Name"` → the name that appears in commit metadata.
- `user.email "you@example.com"` → the email associated with your commits.
- `color.ui auto` → enables colored output when in a terminal.

### Config Scopes

| Scope | Storage Location | Applies To |
|-------|------------------|------------|
| `--system` | `/etc/gitconfig` | Every user on the machine |
| `--global` | `~/.gitconfig` | All repos for your user |
| `--local` | `.git/config` | Only the current repo |

**Precedence:** Local > Global > System. So a local setting overrides a global one.

### Viewing Configuration

```bash
git config --list              # Show all settings
git config --global --list     # Show global settings
git config user.name           # Show the current value of user.name
```

### Useful Aliases

An **alias** is a shortcut for a longer command:

```bash
git config --global alias.co checkout    # Now `git co` = `git checkout`
git config --global alias.br branch      # `git br` = `git branch`
git config --global alias.st status      # `git st` = `git status`
git config --global alias.lg "log --oneline --graph --decorate"
```

**Q: What is the difference between `--global` and `--local`?**
**A:** `--global` applies settings to every repository on your machine for your user. `--local` applies only to the current repository. Local settings override global ones.

**Q: Why does Git need user.name and user.email?**
**A:** Every commit records the author. Without them, Git cannot attribute commits correctly.

---

## 6. Creating a Repository

### Detailed Explanation

You can start working with Git in two ways:
1. **Initialize** a new repo from scratch in an existing folder.
2. **Clone** an existing repo from a remote (like GitHub).

### Initialize a New Repo

```bash
git init
git init myproject
```

**What happens:**
- A hidden `.git/` folder is created.
- `.git/` contains all the metadata: objects, refs, config, hooks.
- Your working directory is now **tracked** by Git.

**Important:** `git init` does **not** track any files yet. You must `git add` them.

### Clone an Existing Repo

```bash
git clone https://github.com/user/repo.git
git clone https://github.com/user/repo.git myfolder
git clone -b branch-name https://github.com/user/repo.git
```

**What happens:**
- Downloads the full history of the repository.
- Creates a folder named after the repo (or your chosen name).
- Automatically sets up the `origin` remote pointing back to the URL.
- Checks out the default branch (usually `main`).

**Q: What does `git init` do?**
**A:** Creates a new empty Git repository in the current directory (creates `.git/`).

**Q: What does `git clone` do?**
**A:** Downloads a project with its entire commit history from a remote repository and sets up `origin` as the remote.

**Q: Difference between `git init` and `git clone`?**
**A:** `git init` starts a brand-new repo locally. `git clone` copies an existing repo from a remote URL.

---

## 7. Basic Workflow — Add, Commit, Status

### Detailed Explanation

The day-to-day Git workflow has three steps:
1. **Edit** files in your working directory.
2. **Stage** changes you want to include in the next commit (`git add`).
3. **Commit** the staged changes with a message (`git commit`).

### Check Status

```bash
git status
git status -s              # Short format
git status --ignored       # Include ignored files
```

**`git status` shows:**
- Current branch name
- Which files are **untracked** (new, not in Git yet)
- Which files are **modified** (changed but not staged)
- Which files are **staged** (ready to be committed)
- Whether your branch is ahead or behind its remote

**Short format example:**
```
 M file1.txt       # Modified, not staged
M  file2.txt       # Staged
?? file3.txt       # Untracked
```

### Stage Files

```bash
git add file.txt           # Stage one file
git add .                  # Stage everything in this directory
git add *.txt              # Stage all .txt files
git add -A                 # Stage all changes (including deletions)
git add -p                 # Stage interactively (patch mode)
```

**What staging does:** It copies the current version of the file into the staging area (index). This is the version that will be included in the next commit.

### Commit

```bash
git commit -m "Add login feature"           # Standard commit
git commit -am "Fix bug"                    # Stage tracked + commit in one step
git commit --amend                          # Modify the last commit
git commit --amend --no-edit                # Amend without changing the message
```

**What a commit contains:**
- A unique SHA-1 hash (e.g., `c87e6ae4...`)
- The author's name and email
- A timestamp
- A commit message
- A pointer to the previous commit (parent)
- A snapshot of all staged files

**Q: What does `git add` do?**
**A:** Stages one or more files for the next commit by copying them into the staging area (index).

**Q: What does `git commit` do?**
**A:** Creates a new commit from staged changes, with a message and metadata (author, timestamp).

**Q: Difference between `git add .` and `git add -A`?**
**A:** `git add .` stages new files and modifications in the current directory only. `git add -A` stages all changes (new, modified, deleted) across the entire repository.

---

## 8. Viewing Changes — diff and log

### Detailed Explanation

### Diff

`git diff` shows you what changed but hasn't been staged or committed yet.

```bash
git diff                    # Working dir vs staging area
git diff --staged           # Staging area vs last commit
git diff HEAD~1             # Working dir vs previous commit
git diff branch1..branch2   # Between two branches
git diff file.txt           # Changes in a specific file
```

**Reading a diff:**
```
- old line
+ new line
```
- `-` = removed
- `+` = added
- A line beginning with a space = unchanged context

### Log

`git log` shows the commit history of the current branch.

```bash
git log                     # Full commit history
git log --oneline           # Compact — one line per commit
git log --graph --decorate  # Visual graph with refs
git log -n 5                # Last 5 commits
git log -p                  # Show patch details
git log --stat              # Show file stats
git log --author="John"     # Filter by author
git log --since="1 week ago"  # Since date
git log --grep="bug"        # Search commit messages
```

**`--graph --decorate` is useful for:**
- Seeing how branches diverge and merge.
- Seeing where tags, HEAD, and remote branches point.

### Show a Specific Commit

```bash
git show HEAD
git show abc1234
git show HEAD~1
```

**Q: What does `git log --oneline` do?**
**A:** Shows a compact commit history — one commit per line (short hash + message).

**Q: How do you see changes between staged and committed?**
**A:** `git diff --staged` or `git diff --cached`.

---

## 9. Branching

### Detailed Explanation

A **branch** is a lightweight movable pointer to a commit. Instead of copying the entire project (like older VCS), Git branches are just 41-byte files that contain a SHA-1 hash.

**Why branches matter:**
- Let you work on features in isolation.
- Multiple people can work on different branches simultaneously.
- Easy to discard a failed experiment — just delete the branch.

### Create and Switch

```bash
git branch feature            # Create branch (stay on current)
git checkout -b feature       # Create AND switch
git switch -c feature         # Modern alternative
git checkout feature          # Switch to existing branch
git switch feature            # Modern switch
```

**`git switch` vs `git checkout`:** `git switch` was introduced in Git 2.23 to make branch switching clearer. `git checkout` is the older, more overloaded command (it does branching, file restoration, and more).

### List Branches

```bash
git branch                    # Local branches
git branch -a                 # All branches (local + remote)
git branch -r                 # Remote branches only
git branch -v                 # With last commit
```

### Delete Branches

```bash
git branch -d feature             # Delete (safe — only if merged)
git branch -D feature             # Force delete (even if unmerged)
git push origin --delete feature  # Delete remote branch
```

### Rename Branches

```bash
git branch -m oldname newname     # Rename a specific branch
git branch -m newname             # Rename the current branch
```

**Q: How do you create a new branch and switch to it immediately?**
**A:** `git checkout -b newbranch` or `git switch -c newbranch`.

**Q: What is a branch?**
**A:** A lightweight movable pointer to a commit — enables parallel development.

**Q: Difference between `git branch` and `git checkout`?**
**A:** `git branch` lists, creates, or deletes branches. `git checkout` switches between branches (or restores files).

---

## 10. Merging & Merge Conflicts

### Detailed Explanation

**Merging** combines changes from one branch into another.

### Merge Workflow

```bash
git checkout main             # Go to target branch
git merge feature             # Merge feature into main
git merge --no-ff feature     # Merge with a merge commit (no fast-forward)
git merge --abort             # Abort a conflicted merge
```

### Fast-Forward vs Three-Way Merge

| Type | When it happens | Result |
|------|-----------------|--------|
| **Fast-forward** | Target branch hasn't changed since the source branch diverged | Main pointer just moves forward |
| **Three-way** | Both branches have new commits | Creates a new "merge commit" with two parents |

### Merge Conflicts

A **merge conflict** happens when:
- Both branches modify the **same part** of the same file.
- One branch deletes a file that the other modifies.

Git can't decide which version to keep, so it inserts **conflict markers**:

```
<<<<<<< HEAD
She plays a lot.
=======
She loves to sleep.
>>>>>>> cats
```

- `<<<<<<< HEAD` → your current branch's version
- `=======` → separator
- `>>>>>>> cats` → incoming branch's version

### Resolving Conflicts

1. Open the conflicted file(s) in your editor.
2. Edit to keep the correct version (either yours, theirs, or a mix).
3. Remove all conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
4. Stage the resolved files: `git add .`
5. Continue the merge: `git merge --continue` (or `git commit`)
6. Or abort the whole merge: `git merge --abort`

**Q: What is a merge conflict?**
**A:** Occurs when Git cannot automatically merge changes because both branches modified the same part of a file.

**Q: How do you resolve a merge conflict?**
**A:** Edit the file, remove conflict markers, choose the correct content, then `git add` and `git commit` (or `git merge --continue`).

**Q: How do you abort a merge?**
**A:** `git merge --abort`.

---

## 11. Remote Repositories & GitHub

### Detailed Explanation

A **remote** is a repository hosted somewhere else — GitHub, GitLab, Bitbucket, or another server. Your local repo can be connected to one or more remotes.

**`origin`** is the default name Git gives to the remote you cloned from. It's just a convention — you can name it anything.

### Managing Remotes

```bash
git remote -v                                       # List remotes + URLs
git remote add origin https://github.com/user/repo.git  # Add remote
git remote remove origin                            # Remove remote
git remote rename old new                           # Rename
git remote set-url origin new-url                   # Change URL
```

`git remote add` takes two arguments:
1. **Remote name** (e.g., `origin`)
2. **Remote URL** (HTTPS or SSH)

**Q: What is a remote?**
**A:** A repository hosted on a server (GitHub, GitLab) that your local repo syncs with.

**Q: What does `origin` mean?**
**A:** The default name for the remote repository you cloned from. It's just a naming convention.

**Q: What does `git remote -v` show?**
**A:** Lists all remotes and their fetch + push URLs.

---

## 12. Pushing, Pulling, and Fetching

### Detailed Explanation

### Push
Uploads your local commits to a remote repository.

```bash
git push origin main              # Push to main
git push -u origin main           # Set upstream + push
git push                          # Push (if upstream set)
git push --tags                   # Push tags
git push --force-with-lease       # Safer force push
```

**`-u` (upstream):** Sets the default remote and branch for your local branch. After this, you can just run `git push` or `git pull` without arguments.

### Pull
Fetches changes from remote **and merges** them into your current branch.

```bash
git pull origin main              # Fetch + merge
git pull                          # Pull (if upstream set)
git pull --rebase                 # Pull with rebase (cleaner history)
```

### Fetch vs Pull

| `git fetch` | `git pull` |
|-------------|------------|
| Downloads changes only | Downloads + merges |
| Does not modify working dir | Modifies working dir |
| Safe — review before merge | Automatic merge |
| `git fetch origin` | `git pull origin main` |

**Why fetch is safer:** You can inspect the incoming changes with `git log HEAD..origin/main` before merging them. `git pull` assumes you want to merge right away.

```bash
git fetch origin
git log HEAD..origin/main         # See what's new
git merge origin/main             # Merge manually
```

**Q: What does `git push` do?**
**A:** Uploads local commits to a remote repository.

**Q: What does `git pull` do?**
**A:** Fetches changes from remote and merges them into your current branch.

**Q: What is the difference between `git fetch` and `git pull`?**
**A:** `git fetch` downloads changes without merging; `git pull` downloads and merges in one step.

**Q: What does `-u` do in `git push -u origin main`?**
**A:** Sets the upstream branch for the current branch, so future `git push` and `git pull` work without arguments.

---

## 13. Undoing Changes

### Detailed Explanation

Git gives you many ways to undo changes depending on **what state** the changes are in.

### Discard Working Directory Changes

```bash
git checkout -- file.txt          # Discard unstaged changes in file
git restore file.txt              # Modern alternative
git restore .                     # Discard all unstaged changes
```

**Use case:** You made changes you don't want and haven't staged them.

### Unstage Files

```bash
git reset HEAD file.txt           # Unstage a file
git restore --staged file.txt     # Modern alternative
```

**Use case:** You `git add`-ed a file but want to remove it from the next commit without deleting the changes.

### Undo Last Commit

```bash
git reset --soft HEAD~1           # Undo commit, keep changes staged
git reset --mixed HEAD~1          # Undo commit, keep changes unstaged (default)
git reset --hard HEAD~1           # Undo commit, DISCARD all changes (dangerous)
```

**HEAD~1 means:** the commit before HEAD.

| Flag | Effect |
|------|--------|
| `--soft` | Moves HEAD back, keeps files in staging area |
| `--mixed` (default) | Moves HEAD back, keeps files in working dir, unstaged |
| `--hard` | Moves HEAD back, discards all changes (dangerous) |

### Revert a Commit (Safe)

```bash
git revert abc1234                # Creates a new commit that undoes abc1234
git revert HEAD
```

**Why revert is safer than reset:** `revert` doesn't rewrite history. It adds a new commit that undoes the target commit's changes. Safe to use on shared/public branches.

### Remove Files

```bash
git rm file.txt                   # Remove file + stop tracking
git rm --cached file.txt          # Untrack but keep file on disk
git clean -n                      # Dry run — show what would be deleted
git clean -f                      # Delete untracked files
git clean -fd                     # Delete untracked files + directories
```

**Q: Difference between `git reset` and `git revert`?**
**A:** `git reset` removes commits from history (rewrites history). `git revert` creates a new commit that undoes a previous one (preserves history). `revert` is safe for shared branches.

**Q: What does `git reset --hard HEAD~1` do?**
**A:** Removes the last commit and discards all changes in the working directory. Very dangerous — cannot be undone easily.

---

## 14. Stashing & Tagging

### Detailed Explanation

### Stashing
**`git stash`** temporarily saves uncommitted changes so you can switch to another branch or task without committing. It "puts changes aside" for later.

**Use case:** You're working on a feature, a colleague asks for help on a bug, but you're not ready to commit your work. Stash it, fix the bug, come back and pop the stash.

```bash
git stash                         # Save changes
git stash save "work in progress" # Save with a message
git stash list                    # List all stashes
git stash pop                     # Apply + remove from stash
git stash apply                   # Apply (keep in stash)
git stash drop                    # Delete a stash
git stash clear                   # Delete all stashes
git stash show -p                 # Show stash diff
```

| Command | Behavior |
|---------|----------|
| `git stash pop` | Applies the latest stash and **removes** it from the list |
| `git stash apply` | Applies the latest stash and **keeps** it in the list |

### Tagging
**Tags** mark specific commits, usually for releases (v1.0.0, v2.1.3, etc.).

```bash
git tag                           # List tags
git tag v1.0.0                    # Lightweight tag
git tag -a v1.0.0 -m "Release"   # Annotated tag
git tag -d v1.0.0                 # Delete local tag
git push origin v1.0.0            # Push specific tag
git push --tags                   # Push all tags
git checkout v1.0.0               # Checkout a tag (detached HEAD)
```

| Type | Description |
|------|-------------|
| **Lightweight** | Just a pointer to a commit. Acts like a branch that doesn't move. |
| **Annotated** | Full object with tagger name, email, date, and message. Recommended for releases. |

**Q: What is `git stash` used for?**
**A:** Temporarily saving uncommitted changes so you can switch branches or pull without committing.

**Q: Difference between `git stash pop` and `git stash apply`?**
**A:** `pop` applies and removes the stash; `apply` applies but keeps it.

**Q: Difference between lightweight and annotated tags?**
**A:** Lightweight is just a pointer. Annotated includes tagger info, date, and message.

---

## 15. Rebasing

### Detailed Explanation

**Rebasing** moves or combines a sequence of commits onto a new base commit. Unlike merging (which creates a merge commit), rebasing **rewrites history** to make it appear linear.

### How It Works

Imagine you have two branches:
```
main:    A---B---C
              \
feature:       D---E
```

**After `git rebase main` on `feature`:**
```
main:    A---B---C
                  \
feature:           D'---E'
```

The `feature` commits (D and E) are replayed on top of `main`'s latest commit (C). New commits D' and E' have new SHA-1 hashes.

### Commands

```bash
git rebase main                   # Rebase current branch onto main
git rebase -i HEAD~3              # Interactive rebase (last 3 commits)
git rebase --continue             # After resolving conflicts
git rebase --abort                # Abort rebase
git rebase --skip                 # Skip a commit
```

### Interactive Rebase Actions

When you run `git rebase -i`, you can edit the list of commits:

| Action | Meaning |
|--------|---------|
| `pick` | Use commit as-is |
| `reword` | Use commit but change message |
| `edit` | Amend the commit |
| `squash` | Combine with previous commit (keep both messages) |
| `fixup` | Combine with previous commit (discard message) |
| `drop` | Remove commit entirely |

### When NOT to Rebase

**Never rebase public/shared branches.** Because rebase rewrites history (changes SHA hashes), anyone who has the old version of the branch will have conflicts trying to sync. Rebasing is only safe for **local** branches.

**Q: When should you NOT rebase?**
**A:** On shared/public branches — it rewrites history and breaks other people's repos.

**Q: What is the difference between merge and rebase?**
**A:** Merge preserves history and creates a merge commit. Rebase creates a linear history by rewriting commits onto a new base.

---

## 16. .gitignore

### Detailed Explanation

A **`.gitignore`** file tells Git which files or directories should **not** be tracked. This is essential for:
- **Build artifacts:** `.exe`, `.o`, `dist/`, `build/`
- **Dependencies:** `node_modules/`, `venv/`
- **Logs:** `*.log`, `logs/`
- **Environment files:** `.env`, `.env.local`
- **OS files:** `.DS_Store`, `Thumbs.db`
- **IDE files:** `.vscode/`, `.idea/`

### Example `.gitignore`

```
# Ignore build output
build/
dist/
*.o
*.exe

# Ignore logs
*.log
logs/

# Ignore environment files
.env
venv/
node_modules/

# Ignore OS files
.DS_Store
Thumbs.db
```

### Syntax Rules

| Pattern | Matches |
|---------|---------|
| `*.log` | All files ending in `.log` |
| `/build` | Only the `build` folder in the root |
| `build/` | Any `build` directory |
| `!important.log` | Exception — do NOT ignore this file |
| `#comment` | A comment |

**Q: What does `.gitignore` do?**
**A:** Tells Git not to track specified files, such as build output and local configuration.

**Q: Does `.gitignore` affect already tracked files?**
**A:** No. It only affects untracked files. You must run `git rm --cached file` to stop tracking a file that's already committed.

---

## 17. GitHub Workflows

### Detailed Explanation

A **workflow** is a set of conventions for how teams use Git and GitHub together.

### Feature Branch Workflow

The most common workflow:

1. Create a branch for each feature: `git checkout -b feature/login`
2. Commit changes to the branch.
3. Push branch to remote: `git push -u origin feature/login`
4. Open a **Pull Request** on GitHub.
5. Team reviews the PR.
6. Merge into `main`.

**Why this is good:** `main` always stays deployable. Features are developed in isolation.

### Fork and Pull Workflow (Open Source)

Used when you don't have write access to the upstream repo:

1. **Fork** the repository on GitHub (creates a copy under your account).
2. **Clone** your fork locally: `git clone https://github.com/YOU/repo.git`
3. **Add upstream:** `git remote add upstream https://github.com/ORIGINAL/repo.git`
4. Create a **feature branch**.
5. Commit and push to **your fork**.
6. Open a **Pull Request** to the **upstream** repo.
7. Maintainer reviews and merges.

**Why this is good:** Contributors don't need write access to the main repo. Maintainers keep control.

### Git Flow

A heavier, more structured workflow:

- `main` — production-ready code
- `develop` — integration branch
- `feature/*` — new features
- `release/*` — release preparation
- `hotfix/*` — urgent fixes to production

**Q: What is the recommended way to propose a change for review?**
**A:** Create a branch, push it, and open a pull request.

**Q: How does an outside contributor propose changes?**
**A:** Fork the repo, commit to a branch in their fork, and open a pull request to the upstream repo.

**Q: What is a pull request?**
**A:** A GitHub feature that lets you propose changes from one branch (or fork) into another, with review, comments, and status checks before merge.

---

## 18. Complete Command Reference (All Commands + Flags)

### Setup and Configuration

| Command | Purpose |
|---------|---------|
| `git config --global user.name "Name"` | Set global name |
| `git config --global user.email "email"` | Set global email |
| `git config --list` | List all config |
| `git config --global core.editor "vim"` | Set editor |
| `git config --global alias.co checkout` | Create alias |

### Getting and Creating Projects

| Command | Purpose |
|---------|---------|
| `git init` | Create new repo |
| `git clone url` | Clone repo |
| `git clone -b branch url` | Clone specific branch |

### Basic Snapshotting

| Command | Purpose |
|---------|---------|
| `git status` | Show status |
| `git status -s` | Short status |
| `git add file` | Stage file |
| `git add .` | Stage all in current dir |
| `git add -A` | Stage all (including deletions) |
| `git add -p` | Interactive staging |
| `git commit -m "msg"` | Commit |
| `git commit -am "msg"` | Stage tracked + commit |
| `git commit --amend` | Amend last commit |
| `git diff` | Working vs staging |
| `git diff --staged` | Staging vs committed |
| `git rm file` | Remove + untrack file |
| `git rm --cached file` | Untrack only |

### Branching and Merging

| Command | Purpose |
|---------|---------|
| `git branch` | List branches |
| `git branch -a` | All branches |
| `git branch name` | Create branch |
| `git checkout name` | Switch branch |
| `git checkout -b name` | Create + switch |
| `git switch name` | Switch (modern) |
| `git switch -c name` | Create + switch (modern) |
| `git branch -d name` | Delete merged branch |
| `git branch -D name` | Force delete |
| `git merge name` | Merge branch |
| `git merge --no-ff name` | Merge with commit |
| `git merge --abort` | Abort merge |
| `git rebase name` | Rebase onto branch |
| `git rebase -i HEAD~n` | Interactive rebase |
| `git cherry-pick hash` | Apply specific commit |

### Sharing and Updating

| Command | Purpose |
|---------|---------|
| `git remote -v` | List remotes |
| `git remote add origin url` | Add remote |
| `git remote remove origin` | Remove remote |
| `git remote set-url origin url` | Change URL |
| `git fetch origin` | Download changes |
| `git pull origin main` | Fetch + merge |
| `git pull --rebase` | Pull with rebase |
| `git push origin main` | Push |
| `git push -u origin main` | Set upstream + push |
| `git push --tags` | Push tags |
| `git push --force-with-lease` | Safe force push |

### Inspection

| Command | Purpose |
|---------|---------|
| `git log` | Commit history |
| `git log --oneline` | Compact log |
| `git log --graph --decorate` | Visual graph |
| `git log -p` | With patches |
| `git log --stat` | With file stats |
| `git show hash` | Show commit |
| `git blame file` | Who changed each line |
| `git reflog` | Reference log |
| `git diff` | Show changes |

### Undoing

| Command | Purpose |
|---------|---------|
| `git checkout -- file` | Discard changes |
| `git restore file` | Discard changes (modern) |
| `git reset HEAD file` | Unstage |
| `git restore --staged file` | Unstage (modern) |
| `git reset --soft HEAD~1` | Undo commit, keep staged |
| `git reset --mixed HEAD~1` | Undo commit, keep working |
| `git reset --hard HEAD~1` | Undo commit, discard all |
| `git revert hash` | Revert commit (safe) |
| `git clean -n` | Dry run cleanup |
| `git clean -f` | Remove untracked |

### Stashing and Tagging

| Command | Purpose |
|---------|---------|
| `git stash` | Stash changes |
| `git stash pop` | Apply + remove |
| `git stash apply` | Apply, keep stash |
| `git stash list` | List stashes |
| `git stash drop` | Delete stash |
| `git tag v1.0` | Lightweight tag |
| `git tag -a v1.0 -m "msg"` | Annotated tag |
| `git tag -d v1.0` | Delete tag |

---

## 19. Multiple Ways to Get the Same Output

### 19.1 Create a new branch and switch
```bash
git checkout -b feature
git switch -c feature
git branch feature && git checkout feature
```

### 19.2 Stage all changes
```bash
git add .
git add -A
git add --all
```

### 19.3 Commit all tracked changes
```bash
git commit -am "message"
git add -u && git commit -m "message"
```

### 19.4 Discard working directory changes
```bash
git checkout -- file.txt
git restore file.txt
```

### 19.5 Unstage a file
```bash
git reset HEAD file.txt
git restore --staged file.txt
```

### 19.6 View compact log
```bash
git log --oneline
git log --pretty=oneline
git log --format="%h %s"
```

### 19.7 Undo last commit (keep changes)
```bash
git reset --soft HEAD~1
git reset --soft HEAD^
```

### 19.8 Get the current branch name
```bash
git branch --show-current
git rev-parse --abbrev-ref HEAD
```

---

## 20. Fill-in-the-Blank Rules

When the question shows part of the command, only write the missing part:

| Question | Answer | NOT |
|----------|--------|-----|
| `git ___ -m "msg"` (save changes) | `commit` | `git commit` |
| `git ___ -b feature` (create + switch) | `checkout` | `git checkout` |
| `git ___ origin main` (upload) | `push` | `git push` |
| `git ___ --oneline` (compact log) | `log` | `git log` |
| `git ___ --staged` (show staged changes) | `diff` | `git diff` |
| `git ___ HEAD~1` (undo commit) | `reset` | `git reset` |
| `git ___ .` (stage all) | `add` | `git add` |
| `git ___ -a v1.0 -m "Release"` (tag) | `tag` | `git tag` |
| `git ___ origin` (download changes) | `fetch` | `git fetch` |

---

## 21. Practice Questions & Answers

### Section A: Git Basics
**Q1.** What is Git?
**Answer:** A distributed version control system for tracking changes in source code.

**Q2.** Who created Git and when?
**Answer:** Linus Torvalds, 2005.

**Q3.** Difference between Git and GitHub?
**Answer:** Git is the DVCS; GitHub is a hosting platform for Git repos.

**Q4.** What are the three areas of Git?
**Answer:** Working directory, staging area (index), and repository.

**Q5.** What does `git init` do?
**Answer:** Creates a new empty Git repository (`.git/` directory).

### Section B: Basic Workflow
**Q6.** How do you stage a file?
**Answer:** `git add file.txt`

**Q7.** How do you commit with a message?
**Answer:** `git commit -m "message"`

**Q8.** What does `git status` show?
**Answer:** Branch name, current commit, staged files, modified files, untracked files.

### Section C: Branching
**Q9.** How do you create a branch and switch to it?
**Answer:** `git checkout -b feature` or `git switch -c feature`.

**Q10.** How do you merge a branch?
**Answer:** `git checkout main && git merge feature`

**Q11.** How do you delete a branch?
**Answer:** `git branch -d feature` (merged) or `git branch -D feature` (force).

### Section D: Remote Repositories
**Q12.** How do you add a remote?
**Answer:** `git remote add origin https://github.com/user/repo.git`

**Q13.** Difference between `git fetch` and `git pull`?
**Answer:** `fetch` downloads only; `pull` downloads and merges.

**Q14.** How do you push to a remote?
**Answer:** `git push -u origin main`

### Section E: Undoing Changes
**Q15.** How do you unstage a file?
**Answer:** `git reset HEAD file.txt` or `git restore --staged file.txt`

**Q16.** Difference between `git reset` and `git revert`?
**Answer:** `reset` rewrites history; `revert` creates a new undo commit.

### Section F: Conflicts & Stashing
**Q17.** What causes a merge conflict?
**Answer:** Both branches modified the same part of a file.

**Q18.** What does `git stash` do?
**Answer:** Temporarily saves uncommitted changes.

---

## 22. Exam-Style Questions

**Q1.** What is the difference between Git and GitHub?
a) They are the same
b) Git is the DVCS; GitHub is a hosting platform that adds collaboration features
c) GitHub replaces Git
d) Git only works with GitHub

**Answer: b**

---

**Q2.** A change should be proposed for review before it enters `main`. What do you do?
a) Commit directly to `main`
b) Create a branch, push it, and open a pull request
c) Email a patch
d) Fork and never merge

**Answer: b**

---

**Q3.** A contributor outside the organization wants to propose a change to a public repository. What do they do?
a) They need write access
b) Fork the repository, commit to a branch in their fork, and open a pull request to the upstream repository
c) They cannot contribute
d) Clone and push directly

**Answer: b**

---

**Q4.** What does a `.gitignore` file do?
a) Deletes files
b) Tells Git not to track specified files
c) Hides files from other users
d) Encrypts files

**Answer: b**

---

**Q5.** A pull request description contains `Closes #42`. What happens?
a) Nothing
b) Issue 42 is automatically closed when the PR merges
c) The issue is deleted
d) The issue is assigned

**Answer: b**

---

**Q6.** Which command stages changes for the next commit?
a) `git commit`
b) `git add`
c) `git push`
d) `git status`

**Answer: b**

---

**Q7.** What command creates a new branch and switches to it immediately?
a) `git branch newbranch`
b) `git checkout -b newbranch`
c) `git merge newbranch`
d) `git switch newbranch`

**Answer: b**

---

**Q8.** How many ways are present in Git to integrate changes from one branch into another?
a) 3
b) 5
c) 2
d) 4

**Answer: c** (merge and rebase)

---

**Q9.** What does `git revert c87e6ae4` do?
a) Has no effect
b) Creates a new commit that undoes the changes from commit c87e6ae4
c) Deletes the commit
d) Resets to that commit

**Answer: b**

---

**Q10.** In the command `git gc`, what does `gc` stand for?
a) Git commit
b) Garbage collection
c) Get changes
d) Global config

**Answer: b**

---

**Q11.** What does `git blame some_file` do?
a) Deletes the file
b) Shows who last modified each line and when
c) Ignores the file
d) Renames the file

**Answer: b**

---

**Q12.** What is the difference between `git pull` and `git fetch`?
**Answer:** `git fetch` downloads changes from remote but does not merge them; `git pull` downloads and merges in one step.

---

**Q13.** What is a merge conflict and how do you resolve it?
**Answer:** A merge conflict occurs when both branches modify the same part of a file. Git inserts conflict markers. Edit the file, choose the correct content, remove markers, then `git add` and `git commit`.

---

**Q14.** What are the key states in Git?
**Answer:** Working Directory → Staging Area → Repository (committed).

---

**Q15.** What is a branch?
**Answer:** A lightweight movable pointer to a commit.

---

**Q16.** What is a commit in Git?
**Answer:** A snapshot of changes with a message, author, and timestamp.

---

**Q17.** What is `git merge`?
**Answer:** Combines changes from one branch into another.

---

**Q18.** What is `git rebase`?
**Answer:** Moves or combines commits onto a new base, creating linear history.

---

**Q19.** What is `git stash`?
**Answer:** Temporarily saves uncommitted changes so you can work on something else.

---

**Q20.** What is a tag in Git?
**Answer:** A marker for a specific commit (e.g., release version).

---

## 23. Quick Reference Cheat Sheet

| Task | Command |
|------|---------|
| Configure name | `git config --global user.name "Name"` |
| Configure email | `git config --global user.email "email"` |
| Create repo | `git init` |
| Clone repo | `git clone url` |
| Check status | `git status` |
| Stage file | `git add file` |
| Stage all | `git add .` |
| Commit | `git commit -m "msg"` |
| Stage + commit | `git commit -am "msg"` |
| View changes | `git diff` |
| View staged changes | `git diff --staged` |
| View log | `git log --oneline` |
| Visual log | `git log --graph --decorate` |
| Create branch | `git branch name` |
| Create + switch | `git checkout -b name` |
| Switch branch | `git checkout name` |
| List branches | `git branch -a` |
| Merge branch | `git merge name` |
| Abort merge | `git merge --abort` |
| Add remote | `git remote add origin url` |
| List remotes | `git remote -v` |
| Fetch changes | `git fetch origin` |
| Pull changes | `git pull origin main` |
| Push changes | `git push -u origin main` |
| Undo commit (keep) | `git reset --soft HEAD~1` |
| Undo commit (discard) | `git reset --hard HEAD~1` |
| Revert commit | `git revert hash` |
| Discard changes | `git checkout -- file` |
| Unstage | `git reset HEAD file` |
| Stash changes | `git stash` |
| Apply stash | `git stash pop` |
| List stashes | `git stash list` |
| Tag release | `git tag -a v1.0 -m "msg"` |
| Push tags | `git push --tags` |
| Interactive rebase | `git rebase -i HEAD~n` |
| Cherry-pick | `git cherry-pick hash` |
| Ignore file | Add to `.gitignore` |
| View current branch | `git branch --show-current` |
| View reflog | `git reflog` |
| Blame file | `git blame file` |
| Help | `git help command` |
| Git version | `git --version` |