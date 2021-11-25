---
title: 上传 GitHub 踩坑
date: 2021-11-25 13:42:33
tags: GitHub
categories: 教程
cover: /img/github_log.png
---

{% note blue 'fas fa-bullhorn' flat %}关于本地项目上传到Github{% endnote %}

# 安装git

[点击这里](https://git-scm.com/downloads)可以进行安装git

# git上传步骤

## 在GitHub上创建一个新仓库，并复制仓库地址

![创建仓库](/img/git_a.png "创建git仓库")

1. 输入仓库的名称
2. 选择私人仓库还是公共仓库
3. 点击创建存储库

![编辑仓库信息](/img/git_b.png "编辑仓库信息")

复制你仓库的地址

![复制仓库地址](/img/git_c.png "复制仓库地址")

## 把云端仓库克隆到本地

进入你想要拉取项目的目录，右键点击 `Git Bash Here` 

![Git Bash Here](/img/git_d.png "Git Bash Here")

输入 `clone` 命令把仓库拉到本地

```cmd
git clone https://github.com/xxx/   注释：clone 后面的网址换成你刚才复制的仓库地址
```
![clone](/img/git_e.png "clone")

把你的项目根目录里面所有的文件复制到这个刚刚的文件夹里（克隆下来的仓库）

## 上传到云端仓库命令

将全部文件添加到暂存区

```cmd
git add .       (注：add 和 . 中间有空格，. 表示全部内容)
```

检查有无文件没有添加到暂存区

```cmd
git status
```

将暂存区内容添加到本地仓库中

```cmd
git commit -m "提交信息"       (注："提交信息" 这里可以更改你想要的备注信息)
```

推送本地分支到origin主机，本地分支要与云端分支一样

```cmd
git push -u origin master       (注：master为分支名称)
```

# 上传时常见错误，踩坑经历

1. 网络问题，毕竟是国外的，上传时可能需要一些魔法，网络质量也一定要好，网速不能慢，不然push的时候会报错

2. `config` 中的用户信息要和云端的用户信息一致，不一致会报错，用户信息包括用户名和邮箱，可以参考以下命令进行更改
```cmd
git config --global user.name "你的用户名"
git config --global user.email 你的邮箱.com
```
如果去掉`--global`参数，只对当前仓库有效

3. 你的项目没有创建本地git仓库，就是一个在你项目根目录名字为.git的隐藏文件夹，可以在你的根目录使用 `git init` 命令创建一个git仓库