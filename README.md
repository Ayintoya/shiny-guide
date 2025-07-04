# A Simple & Effective Git Workflow

## 1. Starting New Work: The Development Branch

Never work directly on the `main` branch. Always create a dedicated, descriptively-named branch for the feature or fix you are working on.

**Action:**
```bash
# 1. Make sure your local 'main' is up-to-date with the remote repository.
git checkout main
git pull origin main

# 2. Create a new branch for your work and switch to it.
#    Examples: 'feat/user-authentication', 'fix/header-bug'
git checkout -b feat/add-timeline-scrolling
