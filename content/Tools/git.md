---
title: "git"
layout: page
date: 2018-01-02
collection: git
---
[TOC]

## 初始化
```shell
git init
```

## 添加文件
```shell
git add fileName
git add .

git commit -m message

# 文件删除
git rm
```

## 查看状态

```shell
# 仓库当前的状态
git status

# 仓库当前log
git log

# reset之后，找不到新版本的 commit id时，可以使用找回log
git reflog

# 查看工作区和版本库里面最新版本的区别
git diff HEAD -- readme.txt
```
## 版本回退

```shell
# 撤销修改
git checkout -- readme.txt

# 撤回指定版本
git reset --hard HEAD
```
## 添加远程仓库

```shell
# 克隆仓库 
git clone git@github.com:michaelliao/gitskills.git

# 绑定远程仓库
git remote add origin git@github.com:michaelliao/learngit.git

# 删除远程仓库
git remote rm <仓库名>

# 远程仓库的改名
git remote rename <原主机名> <新主机名>

#  推送到master分支
 git push -u origin master

# 从某个分支下载
 git pull origin branch
```
## 分支操作

```shell
# 查看当前分支
git branch

# 创建 dev 分支
git branch dev

# 切换到 dev 分支
git checkout dev

# 创建 dev 分支，然后切换到 dev 分支
git checkout -b dev

# 合并dev分支到当前分支
git merge dev

# 删除 dev 分支
git branch -d dev

# 查看分支合并图
git log --graph
```

## 其他操作
```shell
# Git 显示颜色
git config --global color.ui true

# 参看远程主机的网址
git remote -v
```

## 示例：同一文件夹下，同一库的两个版本

```shell
cd output
git init
git checkout -b gh-pages
git add .
git commit -m 'your comment'
# 以下步骤会在 Github 上创建一个空项目后提示
git remote add origin git@github.com:<username>/<projectname>.git
git push -u origin gh-pages
```
回到上层目录

```shell
git init
git add .
git commit -m 'your comment'
# 以下步骤会在 Github 上创建一个空项目后提示
git remote add origin git@github.com:<username>/<projectname>.git
git push -u origin master
```