1:56
JUNE 9
1. What are the alternatives to git for source code version control
Subversion (SVN) – Centralized version control system.

Mercurial – Distributed, similar to Git but simpler in some ways.

Perforce – Often used in game development and large enterprises.

2. 2. What is the difference between git and GitHub/GitLab?
Git – A distributed version control system (software you run locally on your computer).

GitHub / GitLab – Web-based hosting platforms for Git repositories

3. How to initialize a repo and upload to github
How to initialize a repo and upload to GitHub/GitLab
Initialize a repo on command line:
bash
mkdir my-project
cd my-project
git init

Upload to GitHub/GitLab:
Create an empty repo on GitHub/GitLab (via browser — do not add README, .gitignore, or license yet).

Connect and push:
git remote add origin https://github.com/your-username/my-project.git
git add .
git commit -m "Initial commit"
git push -u origin main

How to directly on github
it clone https://github.com/your-username/my-project.git
cd my-project
git add .
git commit -m "Describe your change"
git push

4. what is .gitignore ? sot files in bash 
gitignore – Lists files/folders that Git should not track
the dot files ,show Hidden by default 

5. what is conflict in version control minimizing and resolving 
Conflict – When two or more people change the same lines in the same file, and Git can’t automatically merge the changes.
how to resolve the conflicts 
Keep changes small and focused 
Use short-lived feature branches.
6. naming / documantation conventions 
Branch names: feature/login-page, bugfix/issue-42, main (not master if possible)

Commit messages: Imperative tense, short subject line (≤50 chars), then blank line + details.
Example: Add password validation not Added password validation
Repository naming: lowercase with hyphens (e.g., my-awesome-tool)
README.md: Title, description, setup instructions, usage, contributors, license.
.gitignore: Use standard templates for your language/framework.
License file (e.g., MIT, GPL) – recommended for open source.

does your repo adhere to this ? yes
