# Git and GitHub Refreshing Notes

1. [Link local project to github repository](#link-local-project-to-a-github-repository)
    
2. [Check the linked github repo from local directory](#check-the-github-repo-that-links-to-the-project)
    
3. [git workflow (basic) - updating](#git-workflow)


# Link local project to a github repository 
## Suppose: You already created a repo on GitHub

- Example: `https://github.com/your-username/my-project`
- You also have a project folder **locally** on your computer (with code and files).

You now want to **put your local files into that GitHub repo**.

------

## Step 1: Go to your local project folder

```
cd path/to/your/local/project
```

------

## Step 2: Initialize Git (only the first time)

```
git init
```

This tells Git to start tracking changes inside this folder.

------

## Step 3: Connect your local folder to the GitHub repo

Copy the repo URL from GitHub (HTTPS or SSH). Example:

```
git remote add origin https://github.com/your-username/my-project.git
```

------

## Step 4: Add all your files

```
git add .
```

------

## Step 5: Commit the changes

```
git commit -m "Initial commit - upload my project"
```

------

## Step 6: Push to GitHub

If your GitHub repo is empty:

```
git branch -M main
git push -u origin main
```

If your GitHub repo **already has some files** (like README):

```
git pull origin main --allow-unrelated-histories
git push origin main
```

## Set `main` as the default upstream branch 
1. Switch to the `main branch` locally
```
git checkout main
```
2. Set main as your default upstream branch
```
git branch --set-upstream-to=origin/main main
```
3. (Optional) Delete the `master` branch
git push origin --delete master
git branch -d master
 
4. Summary 
```
git checkout main
git push -u origin main
git config --global init.defaultBranch main
```

## Important: authetication 
if using HTTPs, when push for the first time. It will ask for the github username (e.g., junlinguo) and the password (use the **personal access token**)

# Check the github repo that links to the project 

## Method 1: List all remotes

Run this inside your project folder:

```
git remote -v
```

👉 Example output:

```
origin  https://github.com/your-username/my-project.git (fetch)
origin  https://github.com/your-username/my-project.git (push)
```

- `origin` = the short name (alias).
- The URL = your GitHub repo.

------



## Method 2: Show detailed config for a remote

```
git remote show origin
```

👉 Example output:

```
* remote origin
  Fetch URL: https://github.com/your-username/my-project.git
  Push  URL: https://github.com/your-username/my-project.git
  HEAD branch: main
  Remote branch:
    main tracked
```

This also tells you which branch (`main` here) your local branch is tracking.

------



## Method 3: Look inside Git config file

```
cat .git/config
```

You’ll see something like:

```
[remote "origin"]
    url = https://github.com/your-username/my-project.git
    fetch = +refs/heads/*:refs/remotes/origin/*
```

------

✅ These are useful if you forget *which repo* your local folder is connected to.



# Git workflow



## 1. `git status`

👉 Shows what’s going on in your repo right now.

- Which files are new, changed, or deleted.
- Which files are staged (ready to be committed).

**Example:**

```
git status
```

Output might look like:

```
On branch main
Changes not staged for commit:
  modified:   script.py
  deleted:    old.txt
Untracked files:
  notes.md
```

------



## 2. `git add`

👉 Tells Git: *“I want to include these file changes in the next snapshot (commit).”*

**Examples:**

```
git add file1.py       # add one file
git add folder/        # add all files in a folder
git add .              # add everything (all changes in this folder)
git add -A             # add everything including deletions
```

------



## 3. `git commit`

👉 Saves a **snapshot** of your staged changes with a message.
 Think of it like *“save version with description.”*

**Example:**

```
git commit -m "fix bug in data processing"
```

Now Git has recorded that version of your project.

------



## 4. `git push`

👉 Uploads your commits (changes) from local → GitHub (remote).

**Example:**

```
git push
```

This sends your saved commits to your GitHub repo so they’re online.

------



## 5. `git pull`

👉 Downloads the latest changes from GitHub (remote) → your computer (local).

**Example:**

```
git pull
```

If a teammate added new code to GitHub, this brings it into your local copy.

------



## 6. `git log` (bonus)

👉 Shows the history of commits.

**Example:**

```
git log --oneline
```

Output:

```
a1b2c3d fix typo in README
d4e5f6a add training script
f7g8h9i initial commit
```

------

## Typical Daily Workflow

1. See what’s changed:

   ```
   git status
   ```

2. Stage changes:

   ```
   git add .
   ```

3. Save a snapshot:

   ```
   git commit -m "add new feature X"
   ```

4. Upload to GitHub:

   ```
   git push
   ```

5. Get the latest from GitHub (before you start working or if someone else updated):

   ```
   git pull
   ```
