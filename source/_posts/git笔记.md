---
title: git笔记
date: 2018-05-08 17:17:59
tags: notes
---
>[] :括号 中的内容为可选项，&lt;&gt; :箭头符号中间的内容为必选项
## checkout
### OPTIONS
#### &emsp;git checkout -b|-B&lt;new_branch&gt;[ &lt;start point&gt;]
> Specifying -b causes a new branch to be created as if git-branch(1) were called and then checked out. In this case you can use the \-\-track or \-\-no-track options, which will be passed to git branch. As a convenience, \-\-track without -b implies branch creation; see the description of \-\-track below.

>If -B is given, &lt;new_branch&gt; is created if it doesn’t exist; otherwise, it is reset. This is the transactional equivalent of
#### &emsp;-b &lt;new_branch&gt;
>自动创建分支并切换到新分支
Create a new branch named &lt;new_branch&gt; and start it at &lt;start_point&gt;; see git-branch(1) for details.

#### &emsp;-B &lt;new_branch&gt;
>Creates the branch &lt;new_branch&gt; and start it at &lt;start_point&gt;; if it already exists, then reset it to &lt;start_point&gt;. This is equivalent to running "git branch" with "-f"; see git-branch(1) for details.
## submodule
>子模块是一个独立的git 仓库，如果用第三方需要fork之后使用fork的项目,不然修改的内容没办法同步，只能提交在本地仓库
### COMMANDS
#### &emsp; add [-b &lt;branch&gt;] [-f|--force] [--name &lt;name&gt;] [--reference &lt;repository&gt;] [--depth &lt;depth&gt;] [--] &lt;repository&gt; [&lt;path&gt;]
>添加子模块
#### &emsp; init [--] [&lt;path&lt;…​]
>初始化子模块
#### &emsp; update [--init] [--remote] [-N|--no-fetch] [--[no-]recommend-shallow] [-f|--force] [--checkout|--rebase|--merge] [--reference &lt;repository&gt;] [--depth &lt;depth&gt;] [--recursive] [--jobs &lt;n&gt;] [--] [&lt;path&gt;…​]
>拉取子模块数据数据
### OPTIONS
#### &emsp;--name
>This option is only valid for the add command. It sets the submodule’s name to the given string instead of defaulting to its path. The name must be valid as a directory name and may not end with a /.
## clone
### OPTIONS
#### &emsp; --recurse-submodules[=<pathspec]
>克隆项目完成后自动使用默认配置克隆子模块。如果没有子模块配置则会忽略
>After the clone is created, initialize and clone submodules within based on the provided pathspec. If no pathspec is provided, all submodules are initialized and cloned. Submodules are initialized and cloned using their default settings. The resulting clone has submodule.active set to the provided pathspec, or "." (meaning all submodules) if no pathspec is provided. This is equivalent to running git submodule update --init --recursive immediately after the clone is finished. This option is ignored if the cloned repository does not have a worktree/checkout (i.e. if any of --no-checkout/-n, --bare, or --mirror is given)
