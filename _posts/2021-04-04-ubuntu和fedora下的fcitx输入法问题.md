---
layout:     post
title:      ubuntu和fedora下的fcitx输入法问题
categories: [Linux]
description: 
keywords: fcitx, fedora
---


# 前言
ubuntu 和 fedora 的默认中文输入法均为 ibus，但是这个输入法对与 jetbrains 家的ide均不是特别友好，经常出现输入时候卡顿严重的问题，就不得不安装其他输入法代替。  
但是 fcitx 输入法并不是开箱即用的，安装好之后还需要配置一些东西才能让它正常工作。

# 步骤
1.安装 fcitx：  
    `sudo apt install fcitx-sunpinyin`  
    `sudo dnf install fcitx-sunpinyin`  
    可选安装 fcitx-config-tool  
2.配置:  
    对于 ubuntu 或者其他部分发行版需要添加环境变量。  
`sudo vim /etc/profile`  
在末尾加上

```bash
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```
注销再登陆即可

但是对于 fedora，我发现只增加环境变量就不好使了，重启之后依然无法输入中文。  
经过一番折腾后发现需要配置输入法  
`alternatives --config xinputrc`  
之后选择 fcitx 即可。 