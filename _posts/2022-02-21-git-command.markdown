---
layout:     post
title:      "git命令"
date:       2022-02-21 17:45:00 +0800
author:     "True-Think"
header-img: "img/aurora-2020-02-21.jpg"
catalog: true
tags:
    - 技术
    - git
---
### Command line instructions

##### Git global setup

```
git config --global user.name "xxx"
git config --global user.email "xxx@xxx.xx"
```

##### Create a new repository
新建项目后，在gitlab上创建一个README.md,再clone

```
git clone git@it.xxx.com:xxx/xxx.git
cd manager_tag_matcher
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

##### Existing folder

```
cd existing_folder
git init
git remote add origin git@git.xxx.com:xxx/xxx.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

##### Existing Git repository

```
cd existing_repo
git remote rename origin old-origin
git remote add origin git@it.xxx.com:xxx/xxx.git
git push -u origin --all
git push -u origin --tags
```

### 撤销命令

+ 撤销commit

  ​	**git reset --soft HEAD**

  HEAD^的意思是上一个版本，也可以写成HEAD~1

  如果你进行了2次commit，想都撤回，可以使用HEAD~2

+ 撤销add

  ​	**git rm -r --cached .**

  -r 说明有文件夹，‘.'代表所有，也可指定具体文件

  

  ## 至于这几个参数：

  ## --mixed 

  意思是：不删除工作空间改动代码，撤销commit，并且撤销git add . 操作

  这个为默认参数,git reset --mixed HEAD^ 和 git reset HEAD^ 效果是一样的。

   

  ## --soft  

  不删除工作空间改动代码，撤销commit，不撤销git add . 

   

  ## --hard

  删除工作空间改动代码，撤销commit，撤销git add . 

  注意完成这个操作后，就恢复到了上一次的commit状态。

   

   

  ### 顺便说一下，如果commit注释写错了，只是想改一下注释，只需要：

  git commit --amend

  此时会进入默认vim编辑器，修改注释完毕后保存就好了。

  