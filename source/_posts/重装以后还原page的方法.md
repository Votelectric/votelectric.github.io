---
title: 重装以后还原page的方法
date: 2026-01-17 10:56:31
tags:
---
    放大假了，不折腾会死的。所以我把系统整个重装了一下。
    以下是我在Archlinux WSL上恢复我的hexo页面的思路。

# 安装
`` sudo pacman -S nodejs npm`` 先把nodejs安装好，不过nodejs的从25.2.1更新到了25.3.0，因此需要修改``.github/workflows/pages.yml``里对应的npm版本。运行``npm install -g hexo-cli``后我本以为大功告成，结果``hexo clean``报错
```
ERROR Cannot find module 'hexo' from '/home/arch/website'  
ERROR Local hexo loading failed in ~/website ERROR  
Try running: 'rm -rf node_modules && npm install --force'
```
## 解决报错

先运行提示的命令``rm -rf node_modules && npm install --force`` 

但我这边还是报错，推测问题是出在找不到hexo上。检查``package.json``的dependence是否有“hexo”，还真没有，运行
``npm install hexo --save``下载下来。接着``npx hexo -v``可以看到hexo了。

### Commit
``sudo pacman -S git github-cli openssh``

``ssh-keygen -t ed25519 -C "name@website.com"``
把sshkey上传到github，就可以重新登录commit了

#### 总结
~~没事别重装~~ 使用一个停更许久的主题就像开报废车，虽然能开但不知道什么时候就出点小毛病，比如``package.json``的·依赖项居然没有写hexo。不过我还是很爱这个主题的（逃

