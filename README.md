# git-cheatsheet
Git Command - Cheatsheet
***
## table of content
- [clone and push](#clone-and-push)
- [push existing local repo](#push-existing-local-repo)
- [show git commit version](#show-git-commit-version)
- [undo commit as new commit](#undo-commit-as-new-commit)
- [reset to online repo origin](#reset-to-online-repo-origin)
- [delete files and folder](#delete-files-and-folder)
***
<br>
<br>

## clone and push
1. git config --global user.email "`your_email@gmail.com`"
2. git config --global user.name "`your_username`"
3. git clone `https://github.com/user/repo.git`
4. *cd to git
5. *make changes
6. git add --all
7. git commit -m "`messages`"
8. git push
9. *login github u:`your_username` p:`your_password`
<br>
<br>

## push existing local repo
1. git -b master
2. git add .
3. git commit -m "`messages`"
4. git remote add origin `https://github.com/user/repo.git`
5. git remote -v
6. git push -u origin master -f
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
2. git commit
<br>
<br>

## reset to online repo origin
1. git fetch origin
2. git reset --hard origin/master
<br>
<br>

## delete file and folder
#### **file**
1. git rm `./folder/file.jsx`
#### **folder**
1. git rm `./folder/folder` -r
<br>
<br>