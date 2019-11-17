---
date: 2018-11-7
tag: 
  - git知识点整理
author: hzSilence
location: ShangHai  
---

# git常见命令大全

## 基本命令
```
git init                             //初始化仓库
git status                           //查看工作区状态  
git diff                             //查看修改内容          
将文件添加到git仓库，分两步
git  add readme.txt                  //提交readme.txt文件到仓库
git commit -m "app GPL"              //将文件保存到仓库并写上注释"app GPL"
git log                              //查看提交历史
git reset --hard 1094a               //就是版本号
git reflog                           //查看命令历史
git rm text.txt                      //删除版本库里面的text.txt版本替换工作区的版本
git checkout --text.txt              //用版本库里面的text.txt版本替换工作区的版本
```

## 分支
```
查看远端分支：git branch -r
查看本地分支：git branch
查看所有分支：git branch -a 
创建分支：git branch <name>
切换分支：git checkout <name>
创建+切换分支：git checkout -b <name>
合并某分支到当前分支：git merge <name>
删除本地分支：git branch -d <name>
删除远端分支：git push origin --delete <name>
Git远端已经删除的分支，本地还在显示
git remote show origin       //获取远端分支信息，可以看到本地和远端分支不同的地方
git remote prune origin      //同步远程的分支到本地
```

## 储藏
```
储藏当前修改: git stash
查看储藏:git stash list
应用最新储藏（储藏还在栈中）:git stash apply
应用储藏（储藏还在栈中）:git stash apply stash@{…..}
删除储藏:git stash drop stash@{…..}
重新应用储藏,同时立刻将其从堆栈中移除:git stash pop stash@{..}
```
## 其他
```
强行将本地代码推送到服务器上：git push origin <name> —force
git默认文件不区分大小写：git config core.ignorecase false
将已存在的代码推到远端：
git remote add origin git@github.com:hzSilence/sskk.git
git push -u origin master
```











