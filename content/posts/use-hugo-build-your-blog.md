---
title: "如何使用 Hugo 搭建自己的博客"
date: 2022-04-12T14:13:41+08:00
draft: true
---

今天我们来讲讲如何使用 Hugo 搭建自己的博客。

## 下载 Hugo
首先我们到 [Hugo Release](https://github.com/gohugoio/hugo/releases) 页面根据自己的操作系统版本下载 Hugo，本文以 Windows 为例，我们下载 Windows x64 版本，然后将文件解压到 `D:/software/hugo` 目录下

![20220417210225](https://static.aalmix.com/20220417210225.png)

![20220417210629](https://static.aalmix.com/20220417210629.png)

然后配置一下系统的环境变量，打开电脑的高级系统设置，设置系统变量，在 `PATH`变量后面添加 Hugo 的目录 `D:/software/hugo`，然后保存，关闭系统设置，然后打开命令行，进入 `D:/software/hugo` 目录，执行 `hugo version` 命令验证一下即可，如下图所示：

![20220417211154](https://static.aalmix.com/20220417211154.png)

![20220417211401](https://static.aalmix.com/20220417211401.png)

配置好环境变量后我们就可以在任意一个目录下执行 `hugo` 命令了。

## 创建博客站点
我们可以使用 `hugo new site myblog` 创建一个新的博客站点，然后在 `myblog` 目录下执行 `hugo server` 命令，这样就可以在浏览器中访问了，如下图所示：