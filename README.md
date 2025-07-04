# A Simple & Effective Git Workflow

### 1. Starting New Work: The Development Branch

Never work directly on the `main` branch. Always create a dedicated, descriptively-named branch for the feature or fix you are working on.

# 1. Make sure your local 'main' is up-to-date with the remote repository.

```bash
git checkout main
```
```bash
git pull origin main
```

# 2. Create a new branch for your work and switch to it.
#    Examples: 'feat/user-authentication', 'fix/header-bug'
```bash
git checkout -b feat/add-timeline-scrolling
```

Now you are on a separate branch, feat/add-timeline-scrolling, and can work without affecting the stable main branch.

## 2. Committing and Pushing Your Work
Commit your changes in small, logical chunks. This makes it easier to understand the history and pinpoint where a bug was introduced.

# 1. Stage all your changes for the next commit.
```bash
git add .
```
# 2. Commit the changes with a clear, descriptive message.
#    (See "Commit Message Prefixes" below for conventions)
```bash
git commit -m "feat: add initial timeline component"
```
# 3. Push your branch to the remote repository (e.g., GitHub).
#    The '-u' flag sets the upstream link the first time you push a new branch.
```bash
git push -u origin feat/add-timeline-scrolling
```
