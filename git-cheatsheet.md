# Git Cheatsheet

> Git is a distributed version-control system for tracking source code and collaborating safely.

## Table of Contents
- [Setup & Config](#setup--config)
- [Creating & Cloning](#creating--cloning)
- [Staging & Committing](#staging--committing)
- [Branching](#branching)
- [Merging & Rebasing](#merging--rebasing)
- [Remotes](#remotes)
- [Undoing Changes](#undoing-changes)
- [Stashing](#stashing)
- [Logs & Diff](#logs--diff)
- [Tags](#tags)
- [Submodules](#submodules)

## Setup & Config

| Command | Description |
| --- | --- |
| `git config --global user.name "Name"` | Set the author name for new commits. |
| `git config --global user.email "you@example.com"` | Set the author email for new commits. |
| `git config --global init.defaultBranch main` | Set the default initial branch name. |
| `git config --global core.editor "code --wait"` | Set the editor Git opens for messages. |
| `git config --global --list` | List global Git configuration values. |
| `git config --list --show-origin` | List configuration values and their sources. |

## Creating & Cloning

| Command | Description |
| --- | --- |
| `git init` | Initialize a repository in the current directory. |
| `git init project-name` | Create and initialize a new project directory. |
| `git clone https://example.com/org/repo.git` | Clone a remote repository. |
| `git clone --depth 1 https://example.com/org/repo.git` | Clone only the latest history snapshot. |
| `git status` | Show the working tree and staging-area state. |
| `git status --short` | Show a concise working tree status. |

## Staging & Committing

| Command | Description |
| --- | --- |
| `git add file.txt` | Stage one file for the next commit. |
| `git add .` | Stage new and modified files below the current directory. |
| `git add -p` | Interactively stage selected hunks. |
| `git restore --staged file.txt` | Remove a file from the staging area. |
| `git commit -m "Describe the change"` | Create a commit with a message. |
| `git commit --amend` | Replace the most recent commit. |
| `git commit --amend --no-edit` | Amend the latest commit without changing its message. |
| `git commit -a -m "Describe the change"` | Stage tracked modifications and commit them. |

## Branching

| Command | Description |
| --- | --- |
| `git branch` | List local branches. |
| `git branch -a` | List local and remote-tracking branches. |
| `git branch feature/login` | Create a branch without switching to it. |
| `git switch feature/login` | Switch to an existing branch. |
| `git switch -c feature/login` | Create and switch to a new branch. |
| `git branch -m old-name new-name` | Rename a branch. |
| `git branch -d feature/login` | Delete a fully merged local branch. |
| `git branch -D feature/login` | Force-delete a local branch. |

## Merging & Rebasing

| Command | Description |
| --- | --- |
| `git merge feature/login` | Merge a branch into the current branch. |
| `git merge --no-ff feature/login` | Create a merge commit even when fast-forwarding is possible. |
| `git merge --abort` | Cancel an in-progress merge. |
| `git rebase main` | Replay current-branch commits onto `main`. |
| `git rebase -i HEAD~3` | Interactively edit the last three commits. |
| `git rebase --continue` | Continue a rebase after resolving conflicts. |
| `git rebase --abort` | Cancel an in-progress rebase. |

## Remotes

| Command | Description |
| --- | --- |
| `git remote -v` | List remotes and their URLs. |
| `git remote add origin https://example.com/org/repo.git` | Add a remote named `origin`. |
| `git remote set-url origin https://example.com/org/repo.git` | Change a remote URL. |
| `git fetch origin` | Download remote refs without merging them. |
| `git pull --ff-only` | Fetch and fast-forward the current branch only. |
| `git push -u origin feature/login` | Push a branch and set its upstream. |
| `git push --force-with-lease` | Safely force-push only if the remote is unchanged. |
| `git remote prune origin` | Remove stale remote-tracking references. |

## Undoing Changes

| Command | Description |
| --- | --- |
| `git restore file.txt` | Discard unstaged changes to a tracked file. |
| `git restore --source=HEAD -- file.txt` | Restore a file from the current commit. |
| `git reset HEAD file.txt` | Unstage a file while preserving its changes. |
| `git reset --soft HEAD~1` | Undo the last commit while keeping changes staged. |
| `git reset --mixed HEAD~1` | Undo the last commit while keeping changes unstaged. |
| `git reset --hard HEAD~1` | Discard the last commit and all working changes. |
| `git revert <commit>` | Create a commit that reverses a prior commit. |
| `git clean -nd` | Preview removal of untracked files and directories. |
| `git clean -fd` | Remove untracked files and directories. |

## Stashing

| Command | Description |
| --- | --- |
| `git stash push -m "WIP login"` | Stash tracked changes with a descriptive message. |
| `git stash push -u` | Stash tracked and untracked files. |
| `git stash list` | List saved stashes. |
| `git stash show -p stash@{0}` | Show the patch stored in a stash. |
| `git stash apply stash@{0}` | Apply a stash without removing it. |
| `git stash pop` | Apply and remove the most recent stash. |
| `git stash drop stash@{0}` | Delete a specific stash. |

## Logs & Diff

| Command | Description |
| --- | --- |
| `git log --oneline --graph --decorate --all` | Show a compact graph of all refs. |
| `git log --stat` | Show changed-file statistics for commits. |
| `git log -p -- file.txt` | Show patch history for one file. |
| `git show <commit>` | Display a commit and its patch. |
| `git diff` | Show unstaged changes. |
| `git diff --staged` | Show changes staged for commit. |
| `git diff main...feature/login` | Compare a branch with its merge-base changes. |
| `git blame file.txt` | Show the last commit that changed each line. |

## Tags

| Command | Description |
| --- | --- |
| `git tag` | List local tags. |
| `git tag v1.0.0` | Create a lightweight tag. |
| `git tag -a v1.0.0 -m "Release 1.0.0"` | Create an annotated release tag. |
| `git push origin v1.0.0` | Push one tag to the remote. |
| `git push origin --tags` | Push all local tags. |
| `git tag -d v1.0.0` | Delete a local tag. |
| `git push origin --delete v1.0.0` | Delete a remote tag. |

## Submodules

| Command | Description |
| --- | --- |
| `git submodule add https://example.com/org/lib.git libs/lib` | Add a repository as a submodule. |
| `git clone --recurse-submodules https://example.com/org/repo.git` | Clone a repository and initialize its submodules. |
| `git submodule update --init --recursive` | Initialize and update all nested submodules. |
| `git submodule update --remote` | Update submodules to their configured remote revisions. |
| `git submodule status` | Show each submodule's checked-out revision. |
