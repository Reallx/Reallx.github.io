---
title: "Git 的使用"
date: 2026-02-08
author: "薛路"
summary: "在新电脑上从0-1安装并使用git"
description: "从0-1的git安装与使用教程"
tags: ["VScode", "Git","GitHub"]
showTOC: true
disableAnchoredHeadings: false 
---

> 在新电脑上从0-1配置 Git
> 记录 Git 的安装及使用

---

最近换了新电脑，需要从头开始配置环境。在大学的时候，稀里糊涂用过几次 Git，趁这个重新配环境的机会，记录一下 Git 的安装和使用。

## 一、Git 的安装
**1. 确认电脑中没有 Git**
   在`cmd`中输入`git --version
`
- 如已有版本号，则已安装过 Git
- 如显示`不是内部或外部命令`，则需要安装 Git

**2. 官网下载 Git**
[Git 下载官网](https://git-scm.com/download/win)：选择合适的版本进行下载。
Git 不一定要安装在C盘，安装时的选项：
```text
除了以下选项需要注意，其他都默认即可：
default editor: Use Visual Studio Code as Git's default editor
Adjusting the name of the initial branch: Let Git decide (recommended)
⚠️Adjusting your PATH environment: Git from the command line and also from 3rd-party software 
```

**3. 验证 Git 是否安装成功**
在`cmd`中输入`git --version
`，出现版本号则装成功了。

**4. 第一次使用 Git 的设置（只做一次）**
打开 VScode 项目文件夹，在终端中（PowerShell recommended）先验证Git可用：`git --version
`

- 设置身份：
```bash
git config --global user.name "Your name"
git config --global user.email "你的GitHub邮箱@example.com"
```

- 验证
```bash
输入
git config --global --list
结果：
user.name=Your name
user.email=xxx
```
## 二、Git 的使用
**1. 基础理解**
> Git = 本地版本时间机
> Github = 云端备份 + 协作中心

完整的使用流程总览：
```markdown
远程仓库（GitHub）
        ↑  push
        ↓  pull
本地仓库（.git）
        ↑  commit
        ↓
工作区（你正在编辑的文件）
```

**2. 使用说明**
将根据工作中会使用到 Git 的顺序，介绍其使用。
**1）准备仓库**
方式一、从 GitHub 上 clone 仓库
新建文件夹后，在终端里输入
`git clone 仓库地址`

方式二、本地项目，需要送到 GitHub 上
在项目文件夹中，终端输入：
```bash
git init
git add .
git commit -m "init"
git remote add origin git@github.com:用户名/仓库.git
git push -u origin main
```
这一步的结果是，本地有`.git`；远程有仓库；两边连上线

**2）日常使用**
```bash
传文件到远程仓库：
git status #查看状态
git add .  #保存所有改动
（git add 文件相对路径） #保存指定文件的改动
git commit -m "标签" #提交，保存一个版本至本地
git push #本地提交同步到 GitHub
在第一次 push 时，需要写：git push -u origin main

每次开始工作前：git pull
从远程仓库拉下来最新的项目版本 
```
文件的四种状态：
```markdown
未跟踪（untracked）
↓ git add
已暂存（staged）
↓ git commit
已提交（committed）
↓ git push
已同步（synced）

```

## 三、注意事项
1. Git 和 GitHub 的通信
   HTTPS：每次`git push/pull`时，需要用 Personal Access Token 验证。当这种方式经常被 reset（网络问题），需要使用 SSH 方式。

   SSH：本地有一把私钥，GitHub 存着你的公钥，建立连接时自动验证，不需要输入任何账号密码，直接 remote 即可。配置方式如下：
   ```bash
    生成 Key：ssh-keygen -t ed25519 -C "你的GitHub邮箱@example.com"
    复制公钥：type %USERPROFILE%\.ssh\id_ed25519.pub
    把公钥复制到 Github：GitHub → Settings → SSH and GPG keys → New SSH key
    验证：ssh -T git@github.com
    successful output：
    Hi xxx! You've successfully authenticated...

   ```

