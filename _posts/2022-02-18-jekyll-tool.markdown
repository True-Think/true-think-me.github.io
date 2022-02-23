---
layout: post
title:  "Jekyll安装与快速使用!"
date:   2022-02-21 14:53:00 +0800
categories: jekyll
author: True Think
header-img: "img/hanlai.jpg"
catalog: true
tags:
    - 技术
    - Typora
---

# 配置Jekeyll for windows

需要安装：  
Ruby (version 2.5.0 or higher)  
RubyGems  
nodejs  
GCC & Make

## 1、安装
0) winddows需要在WSL（Windows Subsystem for Linux）上安装运行<sup>[1]</sup>。请在ubuntu for windows的终端上
> sudo apt-get update -y && sudo apt-get upgrade -y 

1) 安装ruby
>sudo apt-add-repository ppa:brightbox/ruby-ng  
>sudo apt-get update  
>sudo apt-get install ruby2.5 ruby2.5-dev build-essential dh-autoreconf

2) 安装gem
> gem update  
> \# 或  
> gem update --system  

2.5) 如果以上都报错，则需要下载手动更新gem<sup>[2]</sup> 解压后进入文件夹，执行  
>ruby setup.rb

3) 安装jekyll
>gem install jekyll bundler

## 2、启动服务
启动jekyll服务<sup>[3]</sup>，在home或其他目录下，新建一个jekyll站点
>jekyll new myblog  
> cd myblog

启动jekyll （可能报错：4000端口被占用）
>bundle exec jekyll serve

或<sup>[4]</sup>
>bundle exec jekyll serve --livereload --port 4001

## 3、进入网页 `http://127.0.0.1:4001/`

## 4、编辑博客
编辑可查看的博客并查看<sup>[5]</sup>。

1. `./_posts` 目录用来放置博文，文件名称格式为 `<date>-<title>.<extension>`  
2. 示例 *Welcome to Jekyll!*  
   源码位置：`./_posts/2016-10-21-welcome-to-jekyll.markdown`
   ```
   ---
   layout: post
   title:  "Welcome to Jekyll!"
   date:   2022-02-18 16:25:38 +0800
   categories: jekyll update
   ---
   ```
   - layout: 表示博文使用的模板名称，对应 `./_layouts/<name>.html` 文件
   - title, date, categories: 分别设置了博文的标题、日期、分类等信息

3. 模板 & 主题  
   主题位置：`~/.gem/ruby/gems/minima-2.0.0/_layouts/`，找到`post.html`文件
4. 发布
5. 扩展

## *引用*
[1] [*Installation via Bash on Windows 10*](https://jekyllrb.com/docs/installation/windows/)  
[2] [*download page*](https://rubygems.org/pages/download)   
[3] [*Quickstart run*](https://jekyllrb.com/docs/)  
[4] [*Error:  Address already in use*](https://stackoverflow.com/questions/25151736/jekyll-2-2-0-error-address-already-in-use-bind2)  
[5] [*Jekyll使用*](https://www.cnblogs.com/baiyangcao/p/jekyll_basic.html#:~:text=Jekyll%20%E6%98%AF%E4%B8%80%E4%B8%AA%E7%BD%91%E7%AB%99%E7%94%9F%E6%88%90%E5%B7%A5%E5%85%B7%EF%BC%8C%E5%8F%AF%E4%BB%A5%E7%94%A8%E6%9D%A5%E5%B0%86%E5%B8%A6%E6%9C%89%E4%B8%80%E5%AE%9A%E6%A0%BC%E5%BC%8F%E7%9A%84%E6%96%87%E6%9C%AC%EF%BC%88%E5%A6%82%EF%BC%9AMarkDown%EF%BC%89%E8%BD%AC%E6%8D%A2%E6%88%90%E9%9D%99%E6%80%81%E7%9A%84HTML%E9%A1%B5%E9%9D%A2%EF%BC%8C%20%E5%B9%B6%E6%8F%90%E4%BE%9B%E4%BA%86Liquid%E6%A8%A1%E6%9D%BF%E5%BC%95%E6%93%8E%E8%BF%9B%E8%A1%8C%E9%A1%B5%E9%9D%A2%E6%B8%B2%E6%9F%93%EF%BC%8C%E7%84%B6%E5%90%8E%E5%8F%AF%E4%BB%A5%E5%B0%86%E7%94%9F%E6%88%90%E7%9A%84%E9%9D%99%E6%80%81%E7%BD%91%E7%AB%99%E5%8F%91%E5%B8%83%E5%88%B0%E5%A6%82,Github%20Page%E7%B1%BB%E4%BC%BC%E7%9A%84%E6%89%98%E7%AE%A1%E7%BD%91%E7%AB%99%E4%B8%8A%EF%BC%8C%20%E5%AE%9E%E7%8E%B0%E8%87%AA%E5%B7%B1%E7%9A%84%E9%A1%B9%E7%9B%AE%E9%A1%B5%E9%9D%A2%EF%BC%8C%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E7%AD%89%E3%80%82%20%E5%AE%9E%E7%8E%B0%E8%87%AA%E5%B7%B1%E7%9A%84%E9%A1%B9%E7%9B%AE%E9%A1%B5%E9%9D%A2%EF%BC%8C%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E7%AD%89%E3%80%82)