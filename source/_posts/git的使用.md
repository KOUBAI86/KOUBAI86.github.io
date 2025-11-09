---
title: git的使用
date: 2025-10-26 17:28:59
tags:
categories: 技术笔记 
---
# Git 核心使用指南
 
Git 是一款**分布式版本控制系统**，核心作用是追踪文件变更、协作开发和回溯历史版本，避免代码丢失或混乱。
 
## 一、基础配置（首次使用必做）
 
安装 Git 后，在桌面点击右键，找到git bash here，打开命令窗口，需设置全局用户信息（关联提交记录）：
 ```c
git config --global user.name "你的名字" # 设置用户名
git config --global user.email "你的邮箱" # 设置邮箱
git config --list # 验证配置是否生效
```
## 二、核心操作流程（本地仓库）
**1. 创建本地仓库**：（1）**自己创建**在项目文件夹执行`git init` ，生成一个  .git文件夹（仓库核心文件）。
（2）**clone别人的项目仓库**在代码托管仓库复制别人的项目地址，用git输入`git clone 项目地址`按回车

**2. 把代码提交到仓库：**

- `git add 文件名` ：提交单个文件到暂存区

- `git add . ` ：追踪当前文件夹所有变更（新增、修改），如果修改了很多文件，这个可以将所有文件提交到暂存区

**3. 提交记录：** `git commit`将暂存区（Stage）的修改永久保存到本地版本库
`git commit -m "提交说明"` ，将暂存区（Stage）的修改永久保存到本地版本库，并添加备注（m为message消息的缩写）

**4. 查看状态：** `git status` ，随时查看文件是否已追踪、是否有未提交变更。

**5. 查看历史：** `git log` ，查看所有提交记录（包含作者、时间、提交说明）。
`git log --stat`,查看所有提交记录（包含作者、时间、提交说明）,以及修改了哪些文件
 
## 三、协作与远程仓库（常用 GitHub/GitLab）
 
**1. 关联远程仓库：** `git remote add origin 远程仓库地址` （如 GitHub 项目的 HTTPS/SSH 链接）。
`git remote -v`,查看本地仓库关联的远程仓库地址，确定是否连接正确

**2. 推送代码：** `git push origin 分支名`将本地分支代码推送到远程仓库
`git push -u origin 分支名` （首次推送加  -u ，后续可简化为  git push ）。

**3. 拉取代码：**

- `git pull origin 分支名` ：拉取远程分支的最新代码到本地（协作前必做，避免冲突）。

- `git clone 远程仓库地址` ：首次下载整个远程仓库到本地。
 
## 四、关键场景处理
 
**版本回溯：** `git reset --hard 提交ID`把代码回退到指定的节点（通过  git log  获取目标版本的ID，谨慎使用，会覆盖本地未提交内容）。​
**分支：** `git branch`,查看当前项目有哪些分支，master（main）主分支由git自动创建，一般用于：保存经过测试的稳定代码，用来在发布新版本的时候使用，如果想要开发新功能一般在master的基础上复制出一个develop分支
 **创建分支：** `git checkout -b 新分支名`这个会创建分支并且切换到该分支 （如  git checkout -b develop ，创建分支并且切换到该分支，用于开发新功能，不影响主分支）。
              `git checkout 分支名`，切换分支
 **分支合并：** 在develop分支开发的新功能后，需要把develop分支的代码合并到master
              首先`git add .`
              再`git commit -m "备注"`
              `git checkout master`
              `git merge develop`，就完成了合并

**解决冲突：** 拉取或合并代码时出现冲突，打开冲突文件，手动修改  <<<<<<< HEAD  到  >>>>>>> 分支名  之间的内容，再重新  add  和  commit 。
