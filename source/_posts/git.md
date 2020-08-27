---
title: Git版本控制工具
date: 2020-08-26 23:41:12
categories: 
           - 工具
tags:
           - git
---

## 1 SVN与Git的区别

### 1.1 集中版本控制SVN

> 所有版本数据都保存在服务器上，协同开发者从服务器上同步更新或上传代码，必须联网操作。

### 1.2 分布式版本控制Git

> 所有版本信息仓库同步到本地和服务器，可以离线在本地提交，只需在联网时push到相应服务器。



## 2 Git基本理论

![git工作流程](https://tva1.sinaimg.cn/large/007S8ZIlly1ggit1zgdcuj30i2084t8x.jpg)

- Workspace：工作区，平时存放项目代码的地方

- index/Stage：暂存区，事实上只是一个文件，保存即将提交的文件列表信息

- Reposiitory：本地仓库，有你提交的所有版本的数据

- Remote：远程仓库，代码托管服务器



## 3 Git基本使用

**克隆远程仓库**

```shell
git clone [url]
```

**初始化项目**

```shell
git init
```

**添加到暂存区**

```shell
git add .
```

**添加到本地仓库**

```shell
git commit -m "info"
```

**添加到远程仓库**

```shell
git push -u origin master 
```

**.gitignore忽略文件**

 ```shell
*.txt      #忽略所有.txt结尾的问价
!lib.txt   #但lib.txt除外
build/     #忽略build下的所有文件
/temp	   #忽略根目录/下所有文件，temp除外
doc/*.txt  #忽略doc/a.txt但不包括doc/bin/a.txt
 ```

**初始化方式**

新建一个仓库，git clone这个仓库，把clone下来的文件内容（包括隐藏文件）全部移到你的项目文件夹中

## 4 分支

**列出分支**

```shell
# 列出本地所有分支
git branch
# 列出所有远程分支
git branch -r
```

**新建分支**

```shell
# 新建分支，但停留在当前分支
git branch [branch-name]
# 切换到该分支【每当切换时，工作目录会自动改变】
git checkout [branch-name]
# 新建并切换到分支
git checkout -r [branch-name]
# 在分支里面修改要add和commit
```

**合并分支**

```shell
# 合并指定分支到当前分支
git merge [branch]
```

**删除分支**

```shell
# 删除本地分支
git branch -d [branch-name]
# 删除远程分支
git branch -dr [branch-name]
```