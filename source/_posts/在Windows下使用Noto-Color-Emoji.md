---
title: 在Windows下使用Noto Color Emoji
date: 2026-01-23 10:11:31
tags:
---
感谢 [reddit文章](https://www.reddit.com/r/Windows11/comments/yyesvn/how_to_change_windows_11_emojis/)。

    请先备份注册表！
在``HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\Fonts``下找到`Segoe UI Emoji`条目并删除

下载我把名字改成SegoeUI Emoji的[Noto Color Emoji](https://raw.githubusercontent.com/Votelectric/votelectric.github.io/refs/heads/main/source/files/NotoColorEmoji-Regular.ttf)，为所有用户安装

重启

~~好了我水完贴了~~ 在floorp和edge下都可以正常显示，我的小狼毫也可以正常识别Noto的emoji
![firefox](https://raw.githubusercontent.com/Votelectric/votelectric.github.io/refs/heads/main/source/images/posts/floorp.png)
Floorp的显示效果
![edge](https://raw.githubusercontent.com/Votelectric/votelectric.github.io/refs/heads/main/source/images/posts/edge.png)
edge的显示效果