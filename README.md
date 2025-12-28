- [WHAT IS GIT](#what-is-git)
  - [Working area](#working-area)
  - [Staging area](#staging-area)
  - [Committed](#committed)
  - [Remote](#remote)
- [What is a Git commit?](#what-is-a-git-commit)
- [Initialize a Git repository](#initialize-a-git-repository)
- [How to add files to the Staging area](#how-to-add-files-to-the-staging-area)
- [How to remove files from the Staging area](#how-to-remove-files-from-the-staging-area)
- [`.gitignore` file](#gitignore-file)
  - [What is .gitignore?](#what-is-gitignore)
  - [Main purposes of `.gitignore`](#main-purposes-of-gitignore)
  - [Very important rule (commonly misunderstood)](#very-important-rule-commonly-misunderstood)
  - [Correct way to stop tracking a file](#correct-way-to-stop-tracking-a-file)
  - [Example `.gitignore` (Python / Flask project)](#example-gitignore-python--flask-project)
- [How to make commits](#how-to-make-commits)
  - [Git Shortcut: commit all tracked files](#git-shortcut-commit-all-tracked-files)
  - [Git Shortcut: commit with a short message](#git-shortcut-commit-with-a-short-message)
  - [A technicality about commits](#a-technicality-about-commits)
- [How to undo local commits](#how-to-undo-local-commits)
  - [git revert](#git-revert)
  - [git reset](#git-reset)
  - [How do you use them?](#how-do-you-use-them)

# WHAT IS GIT

- It's a folder where Git has been initialized. It's where we can run Git commands. It's where we can use Git to keep track of the other files in the folder.
- Git repositories can be local (in your computer) or remote (in someone else’s computer).
- All the Git repository information is stored in a folder called `.git`. When you initialize Git in a folder (such as your project), the `.git` folder is created. We’ll look at what’s inside `.git` shortly, but we can think of `.git` as essentially a database. Git is a tool we use to interact with that database.
- **Working directory -> Staging area -> Committed -> Remote**

```
┌──────────────────┐
│  Working Area    │
│ (Working Tree)   │
│                  │
│  File changes    │
└────────┬─────────┘
         │  git add
         ▼
┌──────────────────┐
│  Staging Area    │
│     (Index)      │
│                  │
│  Ready to commit │
└────────┬─────────┘
         │  git commit
         ▼
┌──────────────────┐
│   Local Repo     │
│   (Committed)   │
│                  │
│  Saved locally   │
└────────┬─────────┘
         │  git push
         ▼
┌──────────────────┐
│   Remote Repo    │
│ (GitHub/GitLab)  │
│                  │
│  Shared code     │
└──────────────────┘
```

```
┌────────────────────┐
│   Remote Repo      │
│ (GitHub / GitLab)  │
└─────────┬──────────┘
          │  git fetch / git pull
          │
          ▼
┌────────────────────┐
│   Local Repo       │
│   (Committed)     │
└─────────┬──────────┘
          │  git reset / git revert
          │
          ▼
┌────────────────────┐
│   Staging Area     │
│     (Index)        │
└─────────┬──────────┘
          │  git restore --staged
          │  git reset HEAD
          ▼
┌────────────────────┐
│   Working Area     │
│  (Working Tree)    │
└────────────────────┘

```

## Working area

- The `.git` folder is inside your project folder. Before we tell Git about a file, we say that file is in the working directory. That is, we’re working with it, but we haven’t stored it in the database yet.

## Staging area

- Let’s say we then make some changes to a file. We can tell Git we want to include those changes in the next commit.

- This adds the file to the staging area.

## Committed

- Once we’ve added all the changed files we want to include in the next commit to the staging area, we can commit them!

- This stores all the new files, and references to all previously committed files, in a new commit.

- Once a file has been committed at least once, Git will start keeping a reference to it in future commits. This is called “tracking”.

## Remote

- A remote is a copy of our local repository stored on another computer.

- At any time we can push our commits to the remote to update it. This serves as a backup in case we lose our local repository. It's also good for collaborating with other developers.

# What is a Git commit?

- A commit is a snapshot of files from a repository1.

- A commit doesn't have to include all of the files in a repository. It can include just a few files, while leaving some others outside of the commit.

- At any point, you can see which files you have in your Working Area and your Staging Area by running this command in the command line:

```
git status
```

# Initialize a Git repository

```
git init
```

# How to add files to the Staging area

- When you have files that you'd like to include in the next commit, you can add them to the **Staging area**.

```
# To add app.py, run this command in the command line:
git add app.py
```

- You can use relative paths to add files as well. Imagine your project file and folder structure looks like this:

```
project/
  | - app.py
  | - file.py
  | - models/
      | - user.py

```

```
git add models/user.py
```

- You can also add whole folders if you'd like to include all their files in the next commit:

```
git add models
```

- To stage all files in the working tree we can use the following command:

```
git add --all
```

- Or we can use this shorter version:

```
git add -A
```

# How to remove files from the Staging area

```
# git recommend
git restore --staged <file>

git reset HEAD <file>
```

- Example: That would remove `models/user.py` from the **Staging Area**, but it would leave it in the **Working Area**. That means that you would not lose any changes you've made.

```
git reset HEAD models/user.py
```

- To discard changes in the working directory, first make sure a file is not in the **Staging Area**. Then, run this command:

```
git checkout -- models/user.py
```

# `.gitignore` file

## What is .gitignore?

- `.gitignore` is a file that tells Git which files or directories it should not track, stage, or commi
- In other words: “These files are not part of the source code. Please ignore them.”

## Main purposes of `.gitignore`

- Prevent tracking unnecessary files
- Protect sensitive information
- Keep the repository clean
- Make collaboration easier

## Very important rule (commonly misunderstood)

- `.gitignore` does NOT affect files that are already tracked.

## Correct way to stop tracking a file

```
git rm --cached config.py
git commit -m "Stop tracking config.py"
```

## Example `.gitignore` (Python / Flask project)

```
# Python
__pycache__/
*.pyc

# Environment
.env
venv/

# Logs
*.log

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db
```

# How to make commits

- Once you've got all the file changes you'd like to commit in your Staging Area, you can make a commit out of them.

```
git commit
```

## Git Shortcut: commit all tracked files

- As we've learned, a file becomes "tracked" when we've added it to a previous commit (and not deleted it from the repository)

- That commits all tracked files, and that means we don't have to git add each of them individually.

```
git commit -a
```

## Git Shortcut: commit with a short message

```
git commit -m "Your message here."
```

- Note that you can chain this with the previous tip, and do:

```
git commit -am "Your message here."
```

## A technicality about commits

- In addition to the changes a commit also stores some metadata, such as the author and date of the commit.

- An important thing that is stored is the parent commit: each commit knows what the previous commit was, and that is how we can construct a sequence of commits.

# How to undo local commits

- There are two ways to undo a commit:

  - By telling Git to create a new commit which exactly undoes the changes of a previous commit (e.g. deleting lines of code instead of adding them).
  - By telling Git to get rid of a commit entirely.

- These are known as `git revert` and `git reset`.

## git revert

- This tells Git to create **a new commit** which exactly undoes the changes of a previous commit.

- This is a **safe undo**. After all, if you decide you didn't want to revert your commit after all, you can revert the revert.

- In addition, when you start sharing your commits with other people, it's normal for contributors to add commits, but it is not normal for contributors to remove commits.

- Therefore you should use git revert in either of the following cases:

  - You want the flexibility to bring back your changes later.
  - You are using a remote repository (more on that soon).

## git reset

- This tells Git to **get rid of a commit entirely**.

- This is not a **safe undo**. It is not possible to bring back your commit after it's been deleted.

- If you're sharing your repository with others, they will have problems when you delete commits.

- Therefore, you can use git reset when both of the following are true:

  - You are sure you never want the commit you're deleting again.
  - You are not sharing the repository with others.

- Would recommend using git revert almost every time!

## How do you use them?

- First, you need to know which commit you want to undo. Usually it's the last commit you've made, but it can be one before that.

- You need to find the c**ommit hash**: a unique identifying code that each commit has.

- We can find it by using `git log`. In this example we've got two commits, and this would be the result:

```
git log

commit ae77aedd4cec3b0a6c130a2699dbb7003257033b (HEAD -> master)
Author: Jose Salvatierra <jose@tecladocode.com>
Date:   Mon Dec 16 12:23:26 2019 +0000

    Added changes to app.py to start the Flask app on Debug mode.

commit 0919fd47cae93ac2003b2865f8ffdd1b72e092d3
Author: Jose Salvatierra <jose@tecladocode.com>
Date:   Fri Dec 13 13:21:19 2019 +0000

    Load environment variables from dotenv file locally.
```

- Next we can pass the first few characters of that to either `git revert` or `git reset`:

```
git revert ae77aedd
```
