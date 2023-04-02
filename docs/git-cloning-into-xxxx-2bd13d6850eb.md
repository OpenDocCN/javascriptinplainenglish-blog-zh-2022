# Git:克隆到“xxxx”

> 原文：<https://javascript.plainenglish.io/git-cloning-into-xxxx-2bd13d6850eb?source=collection_archive---------6----------------------->

![](img/aac98bc492cb778c9baf9f5d046df053.png)

本文记录了使用 git 的一个问题

这些问题如下:

执行 git 克隆 git @ git _ repository _ URL:git _ project . git

克隆到‘git _ project’…它没有移动

故障排除流程:

1.  检查运行 git 命令的服务器是否可以与 git 存储库网络正常通信
2.  ping git_repository_url
3.  telnet git_repository_url 22

该问题是由网络问题引起的。请网络同事添加网络权限，解决问题。

此外，添加几个更常用的 git 命令

# 创建新的代码库

```
# Create a new Git repository in your current directory
$ git init

# Create a new directory and initialize it as a Git repository
$ git init [project-name]

# Download a project and its entire code history
$ git clone [url]
```

# 安装ˌ使成形

```
# Display the current Git configuration
$ git config --list

# Edit the Git configuration file
$ git config -e [--global]

# Set user information when submitting code
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
```

# 添加/删除文件

```
# Add the specified file to the staging area
$ git add [file1] [file2] ...

# Add the specified directory to the staging area, including subdirectories
$ git add [dir]

# Add all files in the current directory to the staging area
$ git add .

# Before adding each change, it will ask for confirmation
# For multiple changes to the same file, multiple submissions can be implemented
$ git add -p

# Delete the workspace file and put this deletion into the staging area
$ git rm [file1] [file2] ...

# Stop tracking the specified file, but the file will remain in the workspace
$ git rm --cached [file]

# Rename the file and put this renamed into the staging area
$ git mv [file-original] [file-renamed]
```

# 代码提交

```
# Submit the staging area to the warehouse area
$ git commit -m [message]

# Submit the specified file in the staging area to the warehouse area
$ git commit [file1] [file2] ... -m [message]

# Submit the changes in the workspace since the last commit, directly to the warehouse area
$ git commit -a

# Show all diff information when submitting
$ git commit -v

# Use a new commit, replacing the previous commit
# If the code does not have any new changes, it is used to rewrite the commit information of the last commit
$ git commit --amend -m [message]

# Redo the last commit and include the new changes in the specified file
$ git commit --amend [file1] [file2] ...
```

# 远程同步

```
# Download all changes from the remote repository
$ git fetch [remote]

# show all remote repositories
$ git remote -v

# Display information about a remote repository
$ git remote show [remote]

# Add a new remote repository and name it
$ git remote add [shortname] [url]

# Fetch changes from remote repo and merge with local branch
$ git pull [remote] [branch]

# Upload the local specified branch to the remote warehouse
$ git push [remote] [branch]

# Forcibly push the current branch to the remote repository, even if there are conflicts
$ git push [remote] --force

# push all branches to remote repository
$ git push [remote] --all
```

# 查看信息

```
# Show files with changes
$ git status

# Display the version history of the current branch
$ git log

# Display the commit history, and the files changed with each commit
$ git log --stat

# Search submission history, by keyword
$ git log -S [keyword]

# Display all changes after a commit, each commit occupies one line
$ git log [tag] HEAD --pretty=format:%s

# Display all changes after a commit, whose "commit description" must match the search criteria
$ git log [tag] HEAD --grep feature

# Display the version history of a file, including file renames
$ git log --follow [file]
$ git whatchanged [file]

# Displays every diff related to the specified file
$ git log -p [file]

# Show last 5 commits
$ git log -5 --pretty --oneline

# Show all users who have submitted, sorted by number of submissions
$ git shortlog -sn

# Displays who modified the specified file and when
$ git blame [file]

# Show differences between staging area and workspace
$ git diff

# Show the difference between the staging area and the last commit
$ git diff --cached [file]

# Show differences between the workspace and the latest commit of the current branch
$ git diff HEAD

# Show differences between two commits
$ git diff [first-branch]...[second-branch]

# Show how many lines of code you wrote today
$ git diff --shortstat "@{0 day ago}"

# Display metadata and content changes for a commit
$ git show [commit]

# Show files that changed from a commit
$ git show --name-only [commit]

# Display the content of a file at a commit
$ git show [commit]:[filename]

# Show the last few commits of the current branch
$ git reflog
```

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***