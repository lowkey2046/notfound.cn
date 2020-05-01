+++
title = "Ubuntu Budgie 18.04 系统安装记录"
author = ["notfound"]
date = 2019-01-01T10:01:00+08:00
tags = ["ubuntu"]
draft = false
+++

记录 [Ubuntu Budgie 18.04](https://ubuntubudgie.org/) 安装过程，方便查阅。

选择最小安装，语言为英文。

## 卸载 avahi-daemon 服务

`avahi-daemon` 造成过网络异常，用处也不大，卸载该服务：

```shell
sudo apt purge avahi-daemon
```

## Privoxy

Privoxy 为 HTTP(S) 代理工具：

```shell
sudo apt install privoxy
```

编辑 `/etc/privoxy/config` ，配置需要代理的网站如 GitHub，默认端口为 8118。

通过设置环境变量 `http(s)_proxy` 可启用代理：

```shell
export http_proxy="http://127.0.0.1:8118"
export https_proxy="http://127.0.0.1:8118"
```


## Git & Vim {#git-and-vim}

安装：

```shell
sudo apt install git vim
```

配置 Git：

```shell
git config --global user.name $NAME
git config --global user.email $EMAIL

git config --global credential.helper cache
git config --global core.editor vim
git config --global core.quotepath false
git config --global diff.tool vimdiff
git config --global difftool.prompt no
git config --global grep.lineNumber true
```

使用 vim 自定义配置：

```shell
git clone https://github.com/$USER/vim-rc ~/.vim
git submodule init
git submodule update
```

打开 vim 执行 `:BundleInstall` 安装依赖。

## oh-my-zsh

```shell
sudo apt install zsh
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

编辑 `~/.zshrc` ，添加 `git` `emacs` `docker` `kubectl` 等。

## Emacs & Spacemacs

### 安装 Emacs

通过 ppa 下载 Emacs 最新版，下载速度太慢，所以启用代理：

```shell
sudo add-apt-repository ppa:kelleyk/emacs
sudo http_proxy="http://127.0.0.1:8118" apt install emacs26
```

### 安装配置 Spacemacs

使用 Spacemacs develop 分支：

```shell
git clone -b develop https://github.com/syl20bnr/spacemacs ~/.emacs.d
```

使用 spacemacs 自定义配置，然后拉取 org 文档：

```shell
git clone https://github.com/$USER/spacemacs.d ~/.spacemacs.d
git clone notfound@notfound.cn:/home/notfound/Documents/org ~/Documents/org
```

设置图标和环境变量(解决输入法切换)：

```shell
sudo vim /usr/share/applications/emacs26.desktop
StartupWMClass=Emacs26
Icon=/home/notfound/.emacs.d/core/banners/img/spacemacs.png
Exec=env LC_ALL=zh_CN.UTF-8 emacs26 %F
```

gtags 跳转：

```shell
sudo apt install global
sudo apt install exuberant-ctags python-pygments
gunzip /usr/share/doc/global/examples/gtags.conf.gz -c > ~/.globalrc
echo "export GTAGSLABEL=ctags" >> ~/.zshrc
```

ag 搜索：

```shell
sudo apt install silversearcher-ag
```

Hugo 博客：

```shell
sudo snap install hugo

git clone notfound@notfound.cn:/home/notfound/Documents/notfound.cn ~/Documents/notfound.cn
git submodule init
git submodule update
```

## 语言

通过图形界面设置语言为中文。

中文字体：

```shell
sudo apt install fonts-wqy-microhei fonts-wqy-zenhei
```

emoji：

```shell
sudo apt install fonts-noto-color-emoji
```


## 搜狗拼音输入法

<https://pinyin.sogou.com/linux/?r=pinyin>


## 网易云音乐

<https://music.163.com/#/download>
安装后发现下拉菜单有点问题。

## 安装驱动

[参考](https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-ubuntu-18-04-bionic-beaver-linux)

```shell
sudo ubuntu-drivers autoinstall
```

## 其他

- `eog` 图片查看工具
- `evince` PDF 阅读器
- `gedit` 文本编辑器
- `gnome-system-monitor/bionic-updates` 系统监视器（任务管理器）
- `google-chrome` [下载](https://dl.google.com/linux/direct/google-chrome-stable%5Fcurrent%5Famd64.deb)
- `htop` 升级版 top
- `nginx`
- `openssh-server`
- `tree` 遍历目录下所有文件
- `nodejs` 参考[安装 NodeJS](https://github.com/nodesource/distributions/blob/master/README.md)
- `docker` 参考[安装 Docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
