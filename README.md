# A Simple & Effective Git Workflow

This guide outlines a straightforward workflow for developing on your own or in a small team. Its main goals are to keep the `main` branch clean, make your project history easy to read, and prevent common mistakes.

## 1. Starting New Work: The Development Branch

Never work directly on the `main` branch. Always create a dedicated, descriptively-named branch for the feature or fix you are working on.

1.  **Make sure your local `main` is up-to-date with the remote repository.**
    ```bash
    git checkout main
    git pull origin main
    ```

2.  **Create a new branch for your work and switch to it.** (e.g., `feat/user-authentication`, `fix/header-bug`)
    ```bash
    git checkout -b feat/add-timeline-scrolling
    ```
    Now you are on a separate branch and can work without affecting the stable `main` branch.

## 2. Committing and Pushing Your Work

Commit your changes in small, logical chunks. This makes it easier to understand the history and pinpoint where a bug was introduced.

1.  **Stage all your changes for the next commit.**
    ```bash
    git add .
    ```

2.  **Commit the changes with a clear, descriptive message.** (See "Keeping Your History Readable" below for conventions).
    ```bash
    git commit -m "feat: add initial timeline component"
    ```

3.  **Push your branch to the remote repository.** The `-u` flag sets the upstream link the first time you push a new branch.
    ```bash
    git push -u origin feat/add-timeline-scrolling
    ```
    Pushing regularly acts as a backup of your work.

### Keeping Your Branch Updated
If other changes get merged into `main` while you're working, you should update your branch to prevent major conflicts later.

1.  **Switch to the `main` branch and pull the latest updates.** (Ensure your current branch is clean by committing or stashing changes first).
    ```bash
    git checkout main
    git pull origin main
    ```

2.  **Switch back to your development branch.**
    ```bash
    git checkout feat/add-timeline-scrolling
    ```

3.  **Rebase your branch on top of the latest changes from `main`.**
    ```bash
    git rebase main
    ```
    Rebasing replays your branch's commits on top of `main`'s latest changes, keeping the history linear and clean. If you encounter merge conflicts, Git will pause and ask you to resolve them.

## 3. Merging Your Feature: The Pull Request (PR)

When your feature is complete, merge it into `main` using a Pull Request (PR). The PR is a place to review changes and serves as a record of the merge.

1.  Go to your repository on GitHub.
2.  Click the **"Compare & pull request"** button for your newly pushed branch.
3.  Give the PR a clear title and a brief description of the changes.
4.  Review the "Files Changed" tab yourself. You will often spot mistakes you missed in your editor.
5.  Click **"Merge pull request"**.
6.  Choose the **"Squash and merge"** option. This combines all of your branch's commits into a single, clean commit on the `main` branch, keeping its history tidy.

## 4. Tagging Releases

Once a significant set of features has been merged, it's good practice to tag that point in history as a versioned release.

1.  **Switch to the `main` branch and pull the newly merged changes.**
    ```bash
    git checkout main
    git pull origin main
    ```

2.  **Create an annotated tag for the new version.**
    ```bash
    git tag -a v0.1.0 -m "First playable build with timeline"
    ```

3.  **Push the tag to the remote repository.**
    ```bash
    git push origin v0.1.0
    ```

## 5. Undoing Mistakes

Sometimes things go wrong. Here’s how to handle common scenarios.

### Quick Rollback to a Previous Version
If a merge breaks the application, you can roll back `main` to the last known-good tag.
**Warning:** This rewrites history. It's generally safe for a solo developer but be cautious in a team.

1.  **Ensure you are on the `main` branch.**
    ```bash
    git checkout main
    ```
2.  **Reset your local `main` branch to match the tag.**
    ```bash
    git reset --hard v0.1.0
    ```
3.  **Force-push to update the remote `main` branch.** Using `--force-with-lease` is safer than `-f` because it won't overwrite work someone else pushed while you were working.
    ```bash
    git push --force-with-lease
    ```

### Reverting a Single Bad Commit
To undo one specific commit without losing other recent changes, `git revert` is the safest option. It creates a *new* commit that is the inverse of the bad one, leaving the project history intact.

1.  **Find the hash of the commit you want to undo** (e.g., from the Git log).
    ```bash
    git log
    ```
2.  **Revert that commit.** This will open an editor for the new commit message.
    ```bash
    git revert <commit-sha>
    ```
3.  **Push the new "revert" commit.**
    ```bash
    git push origin main
    ```

## 6. Keeping Your History Readable

Using conventional prefixes for your commit messages makes your log self-documenting.

| What you’re doing          | Suggested commit prefix |
| :------------------------- | :---------------------- |
| New feature                | `feat:`                 |
| Bug fix                    | `fix:`                  |
| Refactoring / code cleanup | `refactor:`             |
| Documentation / comments   | `docs:`                 |
| Build system or tooling    | `chore:`                |
| Performance improvements   | `perf:`                 |
| Adding or updating tests   | `test:`                 |

You can then view a clean, organized log with:
```bash
git log --oneline --decorate --graph --all
