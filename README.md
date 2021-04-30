# git-cheatsheet
cheatsheet untuk Git Command
***
## Table of Content
- [clone and push](#clone-and-push)
- [delete files and folder](#delete-files-and-folder)
- [reset to online repo origin](#reset-to-online-repo-origin)
***
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

## delete file and folder
### `file`
1. git rm `./folder/file.jsx`
### `folder`
1. git rm `./folder/folder` -r


## reset to online repo origin
1. git fetch origin
2. git reset --hard origin/master
