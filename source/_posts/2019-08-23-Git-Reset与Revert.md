---
title: "Git_Reset与Revert"
date: 2019-08-23
categories: Git 
tags: 
- Git
- 工具
---
Git Reset和Revert的用法与异同
<!-- more -->
# Git

## Reset

恢复版本
```bash
#master v1.0->v2.0->v3.0
git log
#查找v2.0的hashID
git reset <版本hashID>
#master v1.0->v2.0
```

git reset 参数:
```bash
git reset --soft <版本hashID>   #回退版本库(commit提交的地方,暂存区的修改还在)
git reset --mixed <版本hashID>  #回退版本库，暂存区(add提交的地方)
git reset --hard <版本hashID>   #回退版本库，暂存区，工作区。(本地代码也撤回了!!)
```
**警告:谨慎使用参数--hard**

## Revert

Revert不像Reset回滚特定版本,而是**撤销特定提交的操作**.
```bash
git revert -n <版本hashID>
#解决冲突
git revert --continue
#编辑并保存备注文件
```

**注意Revert指令**
此处与Rebase指令类似
```bash
  (all conflicts fixed: run "git revert --continue")
  (use "git revert --abort" to cancel the revert operation)
```

## Reset与Revert的异同

Reset是**回滚特定版本**
Revert是**撤销特定提交的操作**
举个例子:
Reset是穿越时空回到过去(你回到了以前的版本,从头再来)
Revert是改变过去,影响现在.(你还在当前时空,但是一部分人生污点没了:)