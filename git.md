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

