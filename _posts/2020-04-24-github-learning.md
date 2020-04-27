---
layout:     post
title:      "Learning Github"
subtitle:   "GitHub 学习笔记"
date:       2020-04-24
author:     "Eryn"
tags:
    - Github
    - Project
---

参考自[廖雪峰老师博客教程](https://www.liaoxuefeng.com/wiki/896043488029600)
和 [阮一峰老师网络日志](https://www.ruanyifeng.com/blog/2014/06/git_remote.html)   

## 本地工作区操作
### 创建版本库
第一步：创建空目录     
* 创建空目录```mkdir learngit```
* 进入创建的文件夹```cd learngit```
* 查看当前目录（文件夹）```pwd```

第二步： 把目录变成git可以管理的仓库     
* 初始仓库```git init```    
Git创建了仓库，告诉你是个空仓库，目录下多了```.git```的目录，用来跟踪版本库的， 不要随便修改     

第三步：查看仓库状态和difference
* 随时掌握工作区的状态```git status```
* 如果status说文件修改过，可以查看修改内容```git diff <file>```

第四步：添加文件    
* 工作区```Working Directory```
* 版本库```Resository```
* 暂存区```Stage/Index```
* 一定要先add再commit，add是将工作区的文件/要提交的修改添加到暂存区
* commit是一次性把暂存区的所有修改提交到分支
* 可以多次添加```git add <file>```
* add三四个文件后可以一次commit```git commit -m "message"```
### 版本回退
* ```HEAD```指向当前版本
* ```git reset --hard commit_id```
* 查看提交历史```git log```回到过去
* 查看命令历史```git reflog```去到未来

### 丢弃修改
* 丢弃工作区修改```git checkout -- file```
* 撤销暂存区的修改（unstage），放回工作区```git reset HEAD <file>```

### 删除修改
* ```rm <file>```
* 第一个情况：从版本库删除文件```git rm <file>```
* 第二个情况：用版本库的版本替换工作的版本，无论工作区是修改还是删除```git checkout -- <file>```

## 远程仓库操作
情景一：本地创建了仓库后，想要在github创建一个仓库，并且让两个仓库远程同步     
* github上```create a new repo```
* 在本地```<file>```仓库下运行命令来关联一个远程库```git remote add origin https://github.com/Eryn-mk/learngit.git```
* **添加后，远程库的名字默认叫法就是```origin```**
* 将本地库的所有内容推送到远程库```git push -u origin master```
* ```-u```用于第一次推送master分支，git不仅会把本地master分支内容推送到远程新的master分支，还会把本地的master分支和远程的master分支关联起来
* 从此，只要本地做了修改并提交（commit）后，有必要的话就可以通过```git push origin master```将本地master分支的最新修改推送至github

情景二：先创建远程库，然后从远程库克隆       
* 在github上创建repo，```initialize with a README```
* 在本地克隆一个本地库```git clone git@github.com:Eryn-mk/learngit.git```
* 进入gitskills目录看看```cd learngit```,```ls```查看目录下已有的文件
* github支持多种协议，https协议```https://github.com/Eryn-mk/learngit.git/```, 和ssh协议```git://```，后者较快

## 常用命令
* ```git fetch origin master```
* 合并```git rebase origin/master```
* ```git push origin master```将本地的master分支推送到origin主机的master分支。如果后者不存在，则会被新建
* ```git push -u origin master```上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。

## 分支管理

* 查看分支```git branch```
* 创建分支```git branch <name>```
* 切换分支```git checkout <name>```,```git switch <name>```
* 创建+切换分支```git checkout -b <name>```, ```git switch -c <name>```
* 合并某分支到当前分支```git merge <name>```
* 删除分支```git branch -d <name>```

### 分支合并和合并冲突
* 有冲突的时候，手动打开file，看到git标注了不一样的地方，手动合并
* 看分支合并图```git log --graph --pretty=oneline --abbrev-commit```

### rebase
* ```git rebase```
* rebase可以把本地未push的分叉提交历史整理成直线
* rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

### fast foward和禁用
* 通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
* 如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
* 因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。
* 禁用fast foward，合并并生成commit```git merge --no-ff -m "merge with no-off" dev```

## 标签管理
### 创建标签
* 切换到需要打标签的分支，```git tag v1.0```
* 用```git tag <tagname>```新建标签，默认为HEAD，也可以指定一个commit id
* 用```git tag v1.0 <commit id>```对某次提交打上标签
* 用```git tag```查看所有标签
* **标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。**

### 删除和推送标签
* 命令```git push origin <tagname>```可以推送一个本地标签；
* 命令```git push origin --tags```可以推送全部未推送过的本地标签；
* 命令```git tag -d <tagname>```可以删除一个本地标签；
* 命令```git push origin :refs/tags/<tagname>```可以删除一个远程标签。
