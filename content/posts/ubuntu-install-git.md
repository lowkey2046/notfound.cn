+++
title = "Ubuntu 安装配置 Git"
author = ["notfound"]
date = 2018-03-20T23:30:00+08:00
tags = ["git"]
draft = false
+++

系统环境：Ubuntu 16.04

## 安装

```shell
sudo apt install git
```

## 配置 ssh key

```shell
ssh-keygen -t rsa -b 4096 -C "username@example.com"
```

- 密钥类型 rsa
- 密钥长度 4096
- 注释字段为邮箱地址，可随意填写或不填

## 配置用户名、邮箱

```shell
git config --global user.name $USERNAME
git config --global user.email $EMAIL
```

## 配置编辑器

```shell
git config --global core.editor vim
```

- 将默认编辑器设置为 vim

## 配置 diff 工具

```shell
git config --global diff.tool vimdiff
git config --global difftool.prompt no
```

- 设置 diff 工具为 vimdiff
- 启动 diff 工具时不提示工具信息
- 在查看差异时，使用 `git difftool` 命令调用 diff 工具进行双栏对比，可以看到每行变更的字符

## 设置 https 密码保存

```shell
git config --global credential.helper cache
```

- `cache` 将密码保存到内存中，15分钟后删除
- `store` 将密码用 **明文** 的形式存放在磁盘中，Linux 环境默认位置为 `~/.git-credentials`


## 配置 grep

```shell
git config --global grep.lineNumber true
```

- 执行 `git grep` 命令时显示行号

## git status 中文编码

```shell
git config --global core.quotepath false
```

## 允许普通仓库推送代码

```shell
git config --local receive.denyCurrentBranch updateInstead
```

## 其他

- 全局配置文件位置 `~/.gitconfig`
- 项目配置 `.git/config`