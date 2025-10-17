# git-cheatsheet

Git Command - Cheatsheet

---

## table of content

pinned

- [accidentally push unwanted files and want to remove from git history](#accidentally-push-unwanted-files-and-want-to-remove-from-git-history)
- [revert after rebase/merge](#revert-after-rebase-or-merge)
- [undo commit as new commit](#undo-commit-as-new-commit)
- [compare between two commits](#compare-between-two-commits)

---
common
- [set email and name](#set-email-and-name)
- [clone](#clone)
- [push](#push)
- [push existing local repo](#push-existing-local-repo)
- [show git commit version](#show-git-commit-version)
- [reset to online repo origin](#reset-to-online-repo-origin)
- [delete file and folder](#delete-file-and-folder)
- [reset local credential](#reset-local-credential)
- [resolving issue "fatal: refusing to merge unrelated histories" - 1](#if-you-encounter-the-fatal-refusing-to-merge-unrelated-histories-error-even-when-attempting-to-pull-changes-from-the-remote-repository-you-can-try-the-following-steps-to-resolve-the-issue)
- [accidentally commit unwanted files](#accidentally-commit-unwanted-files-and-want-to-back-to-unstaged-area)

---

<br>
<br>

## set email and name

1. set email

   ```bash
   git config --global user.email "your_email@gmail.com"
   ```

2. set username

   ```bash
   git config --global user.name "your_username"
   ```
   <br>
   <br>

## clone

1. clone online repo

   ```bash
   git clone https://github.com/username/repo_name.git
   ```

3. go to repo directory

   ```bash
   cd `repo_name`
   ```
   <br>
   <br>

## push

1. git add --all
2. git commit -m "`messages`"
3. git push
   <br>
   <br>

## push existing local repo

1. create branch

   ```bash
   git checkout -b master
   ```

2. add to git

   ```bash
   git add .
   ```

3. commit

   ```bash
   git commit -m "`messages`"
   ```

4. adding remote repository

   ```bash
   git remote add origin `https://github.com/username/repo_name.git`
   ```

5. show remote rpository

   ```bash
   git remote -v
   ```

6. push commit to repository

   ```bash
   git push -u origin master -f
   ```

<br>
<br>

## show git commit version

#### **by default with long hash**

1. git log

#### **short hash version**

1. git log --abbrev-commit
   <br>
   <br>

## undo commit as new commit

> the safest way without losing commits :)<br> > `git log --abbrev-commit` to show the commit versions

1. git revert --no-commit `commit_version`..HEAD
   <br>
   <br>

## reset to online repo origin

1. git fetch origin
2. git reset --hard origin/master
   <br>
   <br>

## revert after rebase or merge

1. reflog

   ```bash
   git reflog --pretty=short --date=iso
   ```

2. reset to HEAD target (find ur target commit after `git reflog`)

   ```bash
   git reset --hard HEAD@{2}
   ```

   or

   ```bash
   git reset --hard "HEAD@{2}"
   ```

<br>
<br>

## delete file and folder

#### **file**

1. git rm `./folder/file.jsx`

#### **folder**

1. git rm `./folder/folder` -r
   <br>
   <br>

## reset local credential

```bash
git config --local credential.helper ""
```

## bypass husky precommit & prepush (AT YOUR OWN RISK: if you need to push do it ASAP without getting stuck waiting for husky rules haha)

```bash
git commit -m "message" --no-verify
```

```bash
git push --no-verify
```

## If you encounter the "fatal: refusing to merge unrelated histories" error even when attempting to pull changes from the remote repository, you can try the following steps to resolve the issue:

1. Fetch the remote repository's changes without merging them:

   ```bash
   git fetch --all
   ```

2. Create an empty commit to establish a common root for the branches:

   ```bash
   git commit --allow-empty -m "Empty commit"
   ```

3. Merge the remote branch into your new branch using the --allow-unrelated-histories flag:

   ```bash
   git merge origin/main --allow-unrelated-histories
   ```

4. Resolve any merge conflicts if they occur. Use a text editor or Git tools to manually resolve conflicts in affected files.
5. Commit the changes

   ```bash
   git commit -m "Merge unrelated histories"
   ```

6. Push the changes to the remote repository:

   ```bash
   git push origin your-branch
   ```

## accidentally commit unwanted files and want to back to unstaged area

```bash
git reset --soft HEAD^
```

## accidentally push unwanted files and want to remove from git history

> example `.env` file

1. add filename to `.gitignore` file
    > optional : if the file may exist under certain conditions, and want to prevent it from being tracked to git
2. untrack and remove file from commit
   ```bash
   git rm -r --cached .env
   ```
3. commit changes
   ```bash
   git add . && git commit -m "remove unwanted files"
   ```
4. remove file from all git commit history
   ```bash
   git filter-branch --index-filter "git rm -rf --cached --ignore-unmatch .env" HEAD
   ```
   all branches version
   ```bash
   git filter-branch -f --index-filter "git rm -rf --cached --ignore-unmatch .env" -- --all
   ```
6. push to origin to implement removed file to remote git history
   ```bash
   git push --force
   ```
7. clear the backup
   ```bash
   git for-each-ref --format="%(refname)" refs/original/ | xargs -n 1 git update-ref -d
   ```

## compare between two commits
access url 

```
https://github.com/USERNAME/REPO_NAME/compare/SHORT_HASH..SHORT_HASH
```
