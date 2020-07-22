---
title: npm 常用命令
date: 2017-11-14
categories:
- npm
tags:
- npm
---

npm 常用命令
<!--more-->

## npm install moduleNames
安装Node模块

> 注意事项：如果在使用模块的时候不知道其名字，可以通过http://search.npmjs.org网站按照

```shell
npm search indexName    # 索引值找到想要的模块。npm也提供了查询的功能 
```
安装完毕后会产生一个node_modules目录，其目录下就是安装的各个node模块。node的安装分为全局模式和本地模式。一般情况下会以本地模式运行，包会被安装到和你的应用代码统计的本地node_modules目录下。在全局模式下，Node包会被安装到Node的安装目录下的node_modules下。全局安装命令为
```shell
npm install -g moduleName。 # 获知使用npm set global=true来设定安装模式
```
```shell
npm get global  # 可以查看当前使用的安装模式
```

```shell
npm install <name> --save   # 安装的同时，将信息写入package.json中
```
项目路径中如果有package.json文件时，直接使用npm install方法就可以根据dependencies配置安装所有的依赖包这样代码提交到github时，就不用提交node_modules这个文件夹了。

```shell
npm install npm@latest -g   # 更新到最新版本npm
```

## npm view moduleNames
查看node模块的package.json文件夹

> 注意事项：如果想要查看package.json文件夹下某个标签的内容，可以使用
```
npm view moduleName labelName
```
## npm list 
查看当前目录下已安装的node包。同命令npm ll/npm ls/npm la
```shell
npm list -g --depth 0   # 查看深度为0 的全局安装模块 
```
> 注意事项：Node模块搜索是从代码执行的当前目录开始的，搜索结果取决于当前使用的目录中的node_modules下的内容。 npm list parseable=true可以目录的形式来展现当前安装的所有node包

## npm help
查看帮助命令。如果要单独查看install命令的帮助，可以使用的npm help install

## npm view moudleName dependencies
查看包的依赖关系

## npm view moduleName repository.url
查看包的源文件地址
## npm view moduleName engines
查看包所依赖的Node的版本
## npm help folders
查看npm使用的所有文件夹
## npm rebuild moduleName
用于更改包内容后进行重建
## npm outdated 
检查包是否已经过时，此命令会列出所有已经过时的包，可以及时进行包的更新
## npm update moduleName
更新node模块
## npm uninstall moudleName
卸载node模块



更多[https://npmjs.org/doc/](https://npmjs.org/doc/)