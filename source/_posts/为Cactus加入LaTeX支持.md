---
title: 为Cactus加入LaTeX支持
date: 2026-01-10 09:54:47
tags:
---
# 引言
Cactus是很老的主题了，很多教程都不适用，本文完全照搬了[为 Hexo 的任何主题添加数学公式（LaTeX）的支持](https://blog.homurax.com/2022/08/21/hexo-theme-latex/)，但是他用的模板引擎是jade，而我的是ejs。所以又扔进Gemini问了一会才折腾出来，就是上一篇Math Test的效果了。

# 准备
(本文默认使用hexo8+nodejs25的组合)
```
npm uninstall hexo-renderer-marked --save    
npm install hexo-renderer-markdown-it --save
npm install @iktakahiro/markdown-it-katex --save
```
先把默认的渲染器换掉，安装markdown-it和katex依赖，@iktakahiro/markdown-it-katex 解决了原生 markdown-it-katex 的 XSS 漏洞，所以这里改用这个版本。
在这之后我的npm开始报错`2 moderate severity vulnerabilities. To address all issues, run:npm audit fix`
在查询过gemini后给出的解决方法是强制使用最新的katex。
打开`package.json`，加入overrides字段：
```
"overrides": {
    "katex": "^0.16.21"
  }
```
我再执行一次`npm install`就没有问题了，如果你出现问题的话，执行多次`npm audit --force`就可以了。

# 改主题
在 `_config.yml` 下加入或修改markdown字段：
```
markdown:
  render:
    html: true
    xhtmlOut: false
    breaks: true
    linkify: true
    typographer: true
    quotes: '“”‘’'
  plugins:
    - "@iktakahiro/markdown-it-katex"
```
然后打开 `themes/cactus/layout/_partial/head.ejs` 在head头的中间加入：
```
<% if (page.mathjax || page.katex) { %>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.21/dist/katex.min.css">
<% } %>
```

由于更换了渲染引擎，在测试之前请先运行`hexo clean`后再hexo g和s

# 代价？
牢主题万年不更的代价就是这样，想用新东西必须自己搓，日后更新维护起来也容易出毛病。~~所以都去用Next吧（逃~~