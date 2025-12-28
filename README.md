- [WHAT IS GIT](#what-is-git)
  - [Working area](#working-area)
  - [Staging area](#staging-area)
  - [Committed](#committed)
  - [Remote](#remote)
- [What is a Git commit?](#what-is-a-git-commit)
- [How to add files to the Staging area](#how-to-add-files-to-the-staging-area)
- [How to remove files from the Staging area](#how-to-remove-files-from-the-staging-area)
- [How to make commits](#how-to-make-commits)
  - [Git Shortcut: commit all tracked files](#git-shortcut-commit-all-tracked-files)
  - [Git Shortcut: commit with a short message](#git-shortcut-commit-with-a-short-message)

# WHAT IS GIT

- It's a folder where Git has been initialized. It's where we can run Git commands. It's where we can use Git to keep track of the other files in the folder.
- Git repositories can be local (in your computer) or remote (in someone else’s computer).
- All the Git repository information is stored in a folder called `.git`. When you initialize Git in a folder (such as your project), the `.git` folder is created. We’ll look at what’s inside `.git` shortly, but we can think of `.git` as essentially a database. Git is a tool we use to interact with that database.
- **Working directory -> Staging area -> Committed -> Remote**

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
