---
title: git笔记
date: 2018-05-08 17:17:59
categories:
- shell
tags: 
- notes
---
>[] :括号 中的内容为可选项，&lt;&gt; :箭头符号中间的内容为必选项

###### add

```
git add . //添加所有文件到git
git add "fileName" //添加指定文件到git
```
###### blame
```
git blame config.rb //显示文件每一行的修改人
```

###### branch
```
git branch //查看本地分支
git branch -a //查看所有分支
git branch test //创建分支
git branch test_branch HEAD^1 //创建分支
git branch test 6444ab774b//在指定ID创建标签
git branch -D test //[-d|-D]删除本地分支
```
###### checkout 
```
git checkout master     //取出master版本的head。
git checkout -b test  //创建 并切换分支
git checkout tag_name    //在当前分支上 取出 tag_name 的版本
git checkout -- hello.rb //这条命令把hello.rb从HEAD中签出.
git checkout  master file_name //master 
git checkout  commit_id file_name  //取文件file_name在commit_id时的版本。
git checkout . //这条命令把 当前目录所有修改的文件 从HEAD中签出并且把它恢复成未修改时的样子.
git checkout -b dev/1.5.4 origin/dev/1.5.4 //从远程dev/1.5.4分支取得到本地分支/dev/1.5.4
```
###### commit
```
git commit -m "cmd merge" //提交修改
git commit --amend //修改commit
git commit --date 2017-6-5 //在指定时间提交修改
```
###### config
```
git config user.name SJJ //默认使用--local
git config --local user.name SJJ //设置user.name
git config --global user.name SJJ
git congfig --list //
```
###### clone

```
git clone <url> //clone文件到当前目录
git clone <url> [dir] //clone文件到指定目录
```
###### describe
```
git describe --tags --abbrev=0 //最近一次提交的tag
```
###### diff

```
git diff //查看 working directory 与 staging area 之间的差异
git diff --cached //查看 repository 与 staging area 之间的差异
git diff HEAD //查看 working directory 与 repository 之间的差异
git diff 3c68b87 --stat

```
###### fetch

```
git fetch origin //获取修改
```
###### gitk

```
 gitk --simplify-by-decoration --all
```

###### log

```
git log //显示提交记录直到最初的提交记录或者按q退出
git log -1 --pretty=%h //最近一次提交的 commit id
git log -1 --pretty=%ci //最近一次提交的时间
git log -1 --pretty=%ct //时间戳
```

###### merge
```
git merge hotfix //合并分支
```
###### mv
```
mkdir //创建文件夹
git mv [-v] [-f] [-n] [-k] <source> <destination> //移动或重命名文件，目录或符号链接
git mv *.html src //移动所有以.html 结尾的文件 到 src 目录下
```

###### pull
```
git pull origin master:master //从 origin 拉取master到本地master
```

###### push 
```
git push origin test_branch:test_branch
git push origin --delete <branchName> //删除远程分支
```
###### rebase
```
git rebase origin/master
git rebase feature
git rebase master feature
git rebase --onto master wrong_branch readme-update
```
###### reflog

```
git reflog //显示HEAD记录
```

###### remote

```
git remote //查看远程仓库
git remote -v //查看远程仓库url
git remote add origin https://github.com/githug/githug //添加远程仓库
```

###### reset
```
git reset --hard id   //回退到指定版本 --hard 丢弃指定id 之后的所有修改
git reset --hard HEAD^ //回退一个版本
git reset --hard HEAD~1 //回退一个版本
git reset HEAD to_commit_second.rb //重置指定文件
--soft 参数将上一次的修改放入 staging area
--mixed 参数将上一次的修改放入 working directory
--hard 参数直接将上一次的修改抛弃
```
###### rev-list

```
git rev-list HEAD --count //获取提交次数
```

###### rm

```
git rm --cache "deleteme.rb" //将文件从git删除
```
###### stash

```
git stash //保存修改到暂存区栈
git stash list //显示暂存区列表
git stash pop //弹栈
```

###### status

```
git status //查看当前状态
```
###### tag

```
git tag //显示tag
git tag "tag_name" //创建临时标签
```



###### .gitignore

```
*.a //正则 匹配 忽略所有以.a 结尾的文件
!a.a //a.a文件不忽略
```


## submodule
>子模块是一个独立的git 仓库，如果用第三方需要fork之后使用fork的项目,不然修改的内容没办法同步，只能提交在本地仓库
### COMMANDS
#### &emsp; add [-b &lt;branch&gt;] [-f|\-\-force] [\-\-name &lt;name&gt;] [\-\-reference &lt;repository&gt;] [\-\-depth &lt;depth&gt;] [\-\-] &lt;repository&gt; [&lt;path&gt;]
>添加子模块
#### &emsp; init [\-\-] [&lt;path&lt;…​]
>初始化子模块
#### &emsp; update [\-\-init] [\-\-remote] [-N|\-\-no-fetch] [\-\-[no-]recommend-shallow] [-f|\-\-force] [\-\-checkout|\-\-rebase|\-\-merge] [\-\-reference &lt;repository&gt;] [\-\-depth &lt;depth&gt;] [\-\-recursive] [\-\-jobs &lt;n&gt;] [\-\-] [&lt;path&gt;…​]
>拉取子模块数据数据
### OPTIONS
#### &emsp;\-\-name
>This option is only valid for the add command. It sets the submodule’s name to the given string instead of defaulting to its path. The name must be valid as a directory name and may not end with a /.
## clone
### OPTIONS
#### &emsp; \-\-recurse-submodules[=<pathspec]
>克隆项目完成后自动使用默认配置克隆子模块。如果没有子模块配置则会忽略
>After the clone is created, initialize and clone submodules within based on the provided pathspec. If no pathspec is provided, all submodules are initialized and cloned. Submodules are initialized and cloned using their default settings. The resulting clone has submodule.active set to the provided pathspec, or "." (meaning all submodules) if no pathspec is provided. This is equivalent to running git submodule update \-\-init \-\-recursive immediately after the clone is finished. This option is ignored if the cloned repository does not have a worktree/checkout (i.e. if any of \-\-no-checkout/-n, \-\-bare, or \-\-mirror is given)



# 