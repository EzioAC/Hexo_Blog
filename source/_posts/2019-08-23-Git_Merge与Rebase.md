---
title: "Git_Merge与Rebase"
date: 2019-08-23
categories: Git 
tags: 
- Git
- 工具
---
Git Merge语句和Rebase语句的用法和异同
<!-- more -->
# Git

## Merge

**Merge(合并)**
```bash
git merge <分支名>
```
**示例**

```bash
#当前节点iss001 v1.0->fixed iss001
#当前主节点master v1.0->v2.0
#在master操作
git merge iss001
#1.修改文件去重
#2.git add XXX
#3.提交
git commit -m "v2.0 with iss001 fixed"
#查看节点历史
git log --graph --pretty=oneline --abbrev-commit
# v1.0  ->v2.0          -> v2.0 with iss001 fixed
#       ->fixed iss001
```

## Rebase

**Rebase(变基)**

### 合并分支
```bash
git rebase <分支名>
```


**注意 Rebase语句会进入解决冲突状态,注意语句!**
```bash
git rebase --abort #放弃rebase操作
git rebase --skip  #跳过改提交
git rebase --continue #继续rebase操作(可能需要多次解决冲突,不需要用commit指令!!)
```

**示例**
```bash
#当前节点iss001 v1.0->fixed iss001
#当前主节点master v1.0->v2.0
#在iss001操作
git rebase master
#1.修改文件去重
#2.git add XXX
#3.继续rebase
git rebase --continue

#查看节点历史
git log --graph --pretty=oneline --abbrev-commit
#当前节点iss001 v1.0->v2.0-> fixed iss001
#当前主节点master v1.0->v2.0

git checkout master 
#合并分支(quick-forward)
git merge iss001
#查看节点历史
git log --graph --pretty=oneline --abbrev-commit
#当前主节点master v1.0->v2.0->fixed iss001
```

### 合并提交节点
```bash
git rebase [-i]  <提交起点> [<提交终点>]
```
合并节点 -i为交互模式

**示例**
```bash
#当前节点iss001 v1.0->fix iss001->fix iss001 again->fix iss001 again and again!
#(这个逼居然提交了这么多次) :P (太丢人了)
#git log 查看v1.0的HashID
git rebase -i <v1.0的hashID>
#自动打开todo文件

#pick 326f8ca fix iss001
#pick a492df3 fix iss001 again
#pick 199882e fix iss001 again and again
#改为
pick 326f8ca fix iss001
s a492df3 fix iss001 again
s 199882e fix iss001 again and again
#保存,关闭.
#可能需要解决冲突

#自动打开注释文件.
#修改,关闭,保存.
#查看历史
git log
#当前节点iss001 v1.0->fix iss001 once for all
#(不丢人了!):$
```

**更多方式(自己探索~~)**
```bash
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

## Merge与Rebase的异同

同:Merge与Rebase同样能完成合并功能(虽然rebase之后还是要用merge语句:)
异:节点历史不同,rebase是一条直线,merge存在分支.
异:rebase可以用于整合历史节点.

**Rebase语句比Merge复杂,但是节点历史更加的简单明了(一根葱>分支树)**
**Rebase可以完成整合历史节点等功能**


**感谢@jartto和@git-scm**
[彻底搞懂 Git-Rebase](http://jartto.wang/2018/12/11/git-rebase/)
[分支的新建与合并](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6)