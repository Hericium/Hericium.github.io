---
title: MAC安装virtualenv和virtualenvwrapper
date: 2019-03-05 13:17:41
tags: python
---
> 最近在学python,肯定要学安装python环境，virtualenv是用于用于创建相互独立的python虚拟环境。virtualenvwrapper则是对virtualenv提供了简易的命令行封装。


## 1.首先安装virtualenv和virtualenvwrapper

```
  pip install virtualenv
  pip install virtualenvwrapper
```

## 2. 查找virtualenvwrapper.sh的位置

```
  whereis virtualenvwrapper.sh
  // 输出结果 /usr/local/bin/virtualenvwrapper.sh
```

## 3.把它添加到环境变量中

```
  1.vi ~/.zshrc // 我用的是zsh
  2.source  /usr/local/bin/virtualenvwrapper.sh
  3.source ~/.zshrc  // 使配置文件生效 
```
<!-- more -->

## 4. 使用

```
  1.mkvirtualenv product --python=python3.7 // 创建
  2.workon                // 显示所有的环境名称
  3.workon product        // 进入环境
  4.deactivate            // 推出环境
  5.rmvirtualenv          // 移出环境
  6.lsvirtualenv          // 查看所有环境
```

