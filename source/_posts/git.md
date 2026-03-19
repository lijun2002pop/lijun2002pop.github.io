---
title: git使用
tags: 
  - git
categories: 
  - 技术
date: 2026-03-19
---


##### git全局配置

`git config --global user.name "ifan li"`

`git config --global user.email ifan@qq.com`

##### 查看配置

`git config --global --list`



##### 新建仓库

1. 复制远程仓库

​	`git clone <仓库地址>`

2. 创建本地仓库

​    `git init` 在当前目录创建仓库

​	`git init <仓库名> `  创建指定名称仓库



![](assets/image-20240725104100877.png)

##### 添加和提交文件

`git status` 查看状态

`git ls-files` 查看暂存区文件

`git add .` 添加文件到暂存区

`git add .txt` 添加所有.txt文件到暂存区

`git commit -m '提交信息'` 提交文件

`git commit -am '提交信息'` 组合命令 添加到暂存区并提交

##### 删除文件

`git rm file-name` 从工资区和暂存区删除文件

`git rm --cached file-name` 从暂存区删除文件,保留工作区的

##### 回退版本

`git log` 查看记录

`git log --oneline`  查看精简记录

`git reset --soft`   保留工作区，暂存区内容

`git reset --hard`   不保留工作区，暂存区内容

`git reset --mixed`   保留工作区，不保留暂存区内容 (默认选择)

`git reset <ID>`  回退到<ID>版本

`git reset HEAD~`  回退到上个版本，HEAD表示当前版本， **HEAD~ **== **HEAD~1** 回退一个版本

`git reflog` 查看操作记录 —— 回退错误也不怕 查到操作前<ID>,使用`git reset --hard <ID>`  回退

##### 查看差异

`git diff` 查看工作区与暂存区差异

`git diff <ID> <ID>`  查看版本间差异

##### 忽略文件

创建`.gitignore`文件

写入要忽略文件

```txt
1.txt #忽略1.txt文件
*.log #忽略所有.log文件
!info.log#跟踪info.log
build/ #忽略build文件夹
```

##### 本地仓库关联远程仓库

`git remote add origin <远程仓库>`关联远程仓库

`git remote -v ` 查看关联

##### 推送/拉取远程分支

`git push -u origin master:main ` 将本地master分支推送至远程main分支

`git pull origin main:master ` 将远程main分支拉取至本地master分支

##### 分支操作

`git branch ` 查看分支列表

`git branch <name>  `  创建分支

`git checkout <name> ` 切换分支 推荐使用` git switch <name>`

`git merge <name>  `  合并分支 

`git branch -d <name>   `  删除已合并分支

`git branch -D <name>   `  删除未合并分支

`git rebase <name>  `  合并分支,将<name>分支合并到当前分支里，保留提交记录



