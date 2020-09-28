---
title: 使用 Travis 自动部署 Hexo 到 github
date: 2020-09-07 15:35:14
tags: Hexo
categories: Hexo
cover: "https://cdn.jsdelivr.net/gh/jerryc127/CDN@latest/cover/Related_settings_for_Hexo_and_Next_theme.png"
---

# 目的
在搭建完了 hexo 博客之后, 虽然还没正儿八经写博客, 就已经想到了一些骚操作, 每次提交都得先 hexo g, 然后再 push 生成的文件, 这样哪怕是改一个很小的东西都需要重新编译全部文件, 这样就感觉很麻烦, 所以决定使用 <a href="https://link.jianshu.com/?t=https://travis-ci.org/">Travis</a> 来自动持续集成提交到 github 以后的操作。
网上虽然有很多教程, 但是有些步骤比较繁琐, 相对来说, 这个方法是最直接方便的, 所以在这里记录一下。

# 最终实现效果
- 写完文章, 直接 push 到 github source 分支, 其它就不用管了
- 我 hexo 项目中的 .travis.yml 配置文件里监听的就是 source 分支, 所以会触发 webhook
- Travis 则会将该项目 clone 过去, 然后按照 .travis.yml 配置文件中的设置执行接下来的命令
- 执行完成后, 再将编译好的文件发送到自己的服务器, 同时 push 回 master 分支上来
- 这样就可以通过 deangle.github.io 访问我的博客了

# Github 配置
怎么将自己本地的 hexo 项目部署到 github 上这里就不细说了, 网上教程一大堆, 我们直接开始配置。
为了使 Travis 能够将编译好的文件 push 回 github，我们需要生成一个 token, 步骤如下:
1. ![生成 token 入口1](/img/articleImg/generate_token1.png)
2. ![进入生成 token 的页面](/img/articleImg/generate_token2.png)
3. ![生成 token](/img/articleImg/generate_token3.png)
4. ![生成 token](/img/articleImg/generate_token4.png)

# Travis 配置
使用 github 账号登录 Travis, 选择仓库进行配置
1. ![选择项目](/img/articleImg/Travis_setting1.png)
2. ![配置环境变量](/img/articleImg/Travis_setting2.png)

# Terminal
回到终端, 在项目根目录创建 .travis.yml 文件, 并将以下代码添加进去

# 配置代码
```bash
# 使用语言
language: node_js
# node版本
node_js: stable
# 设置只监听哪个分支
branches:
  only:
  - source
# 缓存, 可以节省集成的时间, 这里我用了 yarn, 如果不用可以删除
cache:
  apt: true
  yarn: true
  directories:
    - node_modules
# tarvis 生命周期执行顺序详见官网文档
before_install:
- git config --global user.name "name"
- git config --global user.email "email"
# 由于使用了yarn, 所以需要下载, 如不用 yarn 这两行可以删除
- curl -o- -L https://yarnpkg.com/install.sh | bash
- export PATH=$HOME/.yarn/bin:$PATH
- npm install -g hexo-cli
# 下载 gulp, 不用可以删除
- npm install --save-dev gulp
install:
# 不用yarn的话这里改成 npm i 即可
- yarn
script:
- hexo clean
- hexo generate
- gulp # 不需要的话删除
after_success:
- cd ./public
- git init
- git add --all .
- git commit -m "Travis CI Auto Builder"
# 这里的 REPO_TOKEN 即之前在 Travis 项目的环境变量里添加的 value 值
- git push --quiet --force https://$REPO_TOKEN@github.com/Deangle/Deangle.github.io
  master
```
# 最后
将项目 push 到 github 指定的 source 分支就行了, 过一会就能看见 travis 项目中已经在进行自动部署了