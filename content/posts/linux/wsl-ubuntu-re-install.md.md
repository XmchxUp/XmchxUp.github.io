---
author: "韩立"
title: "WS2L+Ubuntu配置日记"
date: "2022-09-21"
description: "第二次操作失误:cold_sweat:重装了~"
ShowBreadCrumbs: false
tags: ['wsl2', 'ubuntu', '配置']
categories: ['Linux']
---

第一次某个电脑清理软件给我WSL2全删了，第二次nt的去删掉了ubuntu20内置的python3.8(/usr/bin/python3.8、/usr/local/lib/python3.8) 导致包管理错误。[Broken python dependencies after trying to re-install](https://askubuntu.com/questions/1065556/broken-python-dependencies-after-trying-to-re-install)

### 设置root用户的密码
管理员模式打开powershell, 改变ubuntu默认切换的用户  ubuntu2004.exe config --default-user root(这里没用管理员模式又gg了直接打不开ubuntu了), 关闭wsl --shutdown再打开ubuntu修改密码 passwd。最后在改回之前的默认用户ubuntu2204.exe config --default-user tesla。

### 设置代理脚本
proxy
```bash
#!/bin/bash
host_ip=$(cat /etc/resolv.conf |grep "nameserver" |cut -f 2 -d " ")
export ALL_PROXY="http://$host_ip:7980"
```
	source proxy
### WSL2 + Ubuntu 图形化配置~~无缝衔接
[Link](https://cs-learning-every-day.github.io/docs/cs/tools/wsl/gui/)
![image](https://cdn.staticaly.com/gh/XmchxUp/cloudimg@master/20220921/image.3demx18juhy0.webp)

### NvChad
> [安装](https://nvchad.com/quickstart/install#pre-requisites)
- [Install a Nerd Font](https://learn.microsoft.com/en-us/windows/terminal/tutorials/custom-prompt-setup#install-a-nerd-font)
- [Install Nvim](https://github.com/neovim/neovim/wiki/Installing-Neovim)
- https://github.com/craftzdog/dotfiles-public

### Zsh && Oh My Zsh
> [安装](https://zhuanlan.zhihu.com/p/58073103) [插件](https://zhuanlan.zhihu.com/p/61447507)

### Python
设置默认使用python3
```bash
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 1
```
### Git
> [Link](https://cs-learning-every-day.github.io/docs/cs/tools/git/#%e5%a4%9a%e5%8f%b0%e7%94%b5%e8%84%91%e4%bd%bf%e7%94%a8%e4%b8%80%e4%b8%aassh-key)
```shell
sudo apt install git

git config --global user.name "Tesla"
git config --global user.email  "1394466835@qq.com"

```
### Docker
> [Link](https://cs-learning-every-day.github.io/docs/cs/tools/wsl/#wsl%E5%AE%89%E8%A3%85dcoerk)

### Vim
> [Link](https://github.com/archibate/vimrc)