# git-cheatsheet
Git Command - Cheatsheet
***
## table of content
- [set email and name](#set-email-and-name)
- [clone and push](#clone-and-push)
- [push](#push)
- [push existing local repo](#push-existing-local-repo)
- [show git commit version](#show-git-commit-version)
- [undo commit as new commit](#undo-commit-as-new-commit)
- [reset to online repo origin](#reset-to-online-repo-origin)
- [revert after rebase/merge](#revert-after-rebase-or-merge)
- [delete file and folder](#delete-file-and-folder)
- [reset local credential](#reset-local-credential)
- [resolving issue "fatal: refusing to merge unrelated histories" - 1](#if-you-encounter-the-"fatal:-refusing-to-merge-unrelated-histories"-error-even-when-attempting-to-pull-changes-from-the-remote-repository,-you-can-try-the-following-steps-to-resolve-the-issue:)
- [Link to specific section](#if-you-encounter-the-"fatal:-refusing-to-merge-unrelated-histories"-error-even-when-attempting-to-pull-changes-from-the-remote-repository,-you-can-try-the-following-steps-to-resolve-the-issue)


***
<br>
<br>

## set email and name
1. git config --global user.email "`your_email@gmail.com`"
2. git config --global user.name "`your_username`"
<br>
<br>

## clone
1. git clone `https://github.com/username/repo_name.git`
2. cd `repo_name`
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
```shell 
git checkout -b master
```
2. add to git
```shell
git add .
```
3. commit
```shell
git commit -m "`messages`"
```
4. adding remote repository
```shell
git remote add origin `https://github.com/username/repo_name.git`
```
5. show remote rpository
```shell
git remote -v
```
6. push commit to repository
```shell
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
> the safest way without losing commits :)<br>
> `git log --abbrev-commit` to show the commit versions
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
```shell
git reflog --pretty=short --date=iso
```
3. reset to HEAD target (find ur target commit after `git reflog`) 
```shell 
git reset --hard HEAD@{2}
```
or
```shell 
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
```shell
git config --local credential.helper ""
```

## bypass husky precommit & prepush (AT YOUR OWN RISK: if you need to push do it ASAP without getting stuck waiting for husky rules haha)
```shell
git commit -m "message" --no-verify
```
```shell
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


