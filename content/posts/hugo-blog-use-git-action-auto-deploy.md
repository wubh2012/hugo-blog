---
title: "使用hugo搭建博客 - 利用 Github Actions 自动部署网站"
date: 2022-05-25T21:50:44+08:00
draft: true
tags: ["博客", "hugo"]
---

之前我们每次更新博客都需要重新上传 public 这个目录的文件，步骤比较繁琐，今天给大家分享一下我们可以通过 Github Actions 自动部署的方式来更新博客。

## 什么是 GitHub Action

## 怎么使用

依葫芦画瓢，创建一个 `.github/workflow` 这样的目录，然后再创建一个 deploy.yml 文件，内容如下：

```yaml
name: github pages

on: #
  schedule:
    - cron: "0 0 * * *" # every day at midnight
  push: # when a new commit is pushed
    branches:
      - master

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0 # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "0.82.0"
          extended: true

      - name: Setup Node
        uses: actions/setup-node@v2
        with:
          node-version: "12.x"

      - name: Cache dependencies
        uses: actions/cache@v1
        with:
          path: ~/.npm
          key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
          restore-keys: |
            ${{ runner.os }}-node-

      - run: npm i
      - run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          user_name: "github-actions[bot]"
          user_email: "github-actions[bot]@users.noreply.github.com"
```

以后我们每次提后后推送到仓库就会触发自动部署了，而且每天凌晨也会自动部署，这样是不是省事多了 😀 ！
