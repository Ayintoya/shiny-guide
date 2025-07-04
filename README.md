# A Simple & Effective Git Workflow

### 1. Starting New Work: The Development Branch

Never work directly on the `main` branch. Always create a dedicated, descriptively-named branch for the feature or fix you are working on.

### 1. Make sure your local 'main' is up-to-date with the remote repository.

```bash
git checkout main
```
```bash
git pull origin main
```

### 2. Create a new branch for your work and switch to it.
Examples: 'feat/user-authentication', 'fix/header-bug'
```bash
git checkout -b feat/add-timeline-scrolling
```

Now you are on a separate branch, feat/add-timeline-scrolling, and can work without affecting the stable main branch.

### 2. Committing and Pushing Your Work
Commit your changes in small, logical chunks. This makes it easier to understand the history and pinpoint where a bug was introduced.

### 1. Stage all your changes for the next commit.
```bash
git add .
```
### 2. Commit the changes with a clear, descriptive message.
(See "Commit Message Prefixes" below for conventions)
```bash
git commit -m "feat: add initial timeline component"
```
### 3. Push your branch to the remote repository (e.g., GitHub).
The '-u' flag sets the upstream link the first time you push a new branch.
```bash
git push -u origin feat/add-timeline-scrolling
```
Pushing regularly acts as a backup of your work.
Keeping Your Branch Updated
If other changes get merged into main while you're working, you should update your branch to prevent major conflicts later.

### 1. Make sure your branch is clean (commit or stash your changes).
### 2. Switch to the main branch and pull the latest updates.
```bash
git checkout main
```
```bash
git pull origin main
```
### 3. Switch back to your development branch.
```bash
git checkout feat/add-timeline-scrolling
```
### 4. Rebase your branch on top of the latest changes from main.
```bash
git rebase main
```
