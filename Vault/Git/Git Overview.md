## <u>The Mental Model: How Git Actually Works</u>
***Git is a Distributed Version Control System. It doesn't just store files, it stores snapshots of the entire filesystem at points in time.***

### <u>There are 4 Main areas of Git to understand</u>

| Working Directory        | The files you're currently editing on your computer                            |
| ------------------------ | ------------------------------------------------------------------------------ |
| **Staging Area (Index)** | A preparation zone where you pick which changes will go into the next snapshot |
| **Local Repository**     | Your private history timeline                                                  |
| **Remote Repository**    | The shared history (Github, Gitlab, Bitbucket) that the team sees              |
|                          |                                                                                |
### <u> The Daily Workflow </u>
*Commands that will be used 90% of the time*

```bash
git clone <url>
```
- ***What it does:*** Downloads the entire repo, including all history and branches, to your machine.
- ***When to use:*** On your first day or when starting on a new repo.

```bash
git branch <name>
```
- ***What it does:*** Creates a new pointer (branch) to the current commit.

```bash
git switch <name>
```
- ***What it does:*** Moves you to that branch


> [!Important] Why use these?
> NEVER work directly on the main branch (or master). Use "Feature Branches".
> Create a branch for specific task (e.g. feature/login-page).
> 
> ***To create a branch and switch to it in ONE step***
> ```bash
> git checkout -b <name>
> ```
> 


```bash
git add
```
- ***What it does:*** Moves changes from the ***<u>Working Directory </u>*** to the ***<u> Staging Area </u>***.
- ***When to use:*** When you have finished a logical chunk of work.

> [!ERROR] WHEN NOT TO USE
> Do Not use
> ```bash
> git add .
> ```
> blindly if you have untracked config files or secrets (API Keys) that shouldn't be shared.
> 
> 

```bash
git commit -m "write your message here"
```
- **What it does:** Takes the Staging Area and saves it as a permanent snapshot in your **Local Repository**.
- **Why use it:** To save a "save point" in your history.

```bash
git fetch
```
- ***What it does:*** Downloads the latest info from the remote but ***DOES NOT*** change your code.

```bash
git pull
```
- ***What it does:*** Downloads the latest info AND tries to merge it into your current code.

```bash
git push
```
- ***What it does:*** Uploads your current local branch commits to the Remote Repo.
- ***When to use:*** When you're ready to back up your work or open a Pull Request (PR).

### <u> Pro Tools </u>
```bash
git cherry-pick <commit-hash>
```
- ***What it does:*** copies a specific commit from one branch and pastes it onto your current branch.
- ***When to use:*** When you fixed a bug on a different branch and you want that specific fix on main branch without merging the rest of the unfinished branch.

```bash
git reflog
```
- ***What it does:*** Git tracks every movement of the HEAD pointer, even if you deleted branches or did a hard reset.
- ***Why use it:*** if you accidentally did git reset --hard and lost weeks of work, git reflog will show you the hash of where you were before the reset. You can check that hash out and save your career.

```bash
git blame <filename>
```
- ***What it does:*** Shows who modified each line of a file and in which commit

## <u> The Golden Rules </u>
1. ***Never Push Directly to Main:*** Always use a Pull Request (PR) workflow. This allows for code review and automated testing.
2. ***Commit Often, Push Occasionally:*** Commit locally to save your progress. Push when you have a stable unit of work.
3. ***Don't Rewrite Public History:*** If you have pushed a branch that others are using, DO NOT use ***rebase***, ***amend***, or ***reset***. use ***revert*** instead.
4. ***Resolve conflicts locally:*** If your PR has conflicts, pull the latest main into your local branch (or rebase your branch on main), resolve the conflicts on your machine, then push the clean code.