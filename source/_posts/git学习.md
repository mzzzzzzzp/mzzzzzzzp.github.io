---
title: Git学习笔记
date: 2019-5-22 11:53:22
categories: Git
---

# Git
Git是一种分布式版本控制系统，没有中央服务器，每个电脑上都是一个完整的版本库。SVN是集中式版本控制系统，版本库集中放在中央服务器，从服务器获得最新版本，修改后再推送回服务器，需要联网环境。

#### 常用命令
提交
```markdown
git commit
```
创建分支
```markdown
git branch name
```
切换到分支上
```markdown
git checkout name
```

合并分支到主线master上
```markdown
git merge name  //自动创建一个merge，会将commit的实际情况进行记录
git rebase master  //项目历史比较简单，少了merge commit。缺点：当发生冲突时不容易定位问题，
```
相对引用
```markdown
git checkout HEAD~3  //指向倒数第三次父提交的位置
```
强制修改分支位置
```markdown
git branch -f master name  //master指向name分支处
```
撤销修改
```markdown
git reset name  //本地撤销记录到name处
git revert name //远程的也会撤销提交记录到name处 
```