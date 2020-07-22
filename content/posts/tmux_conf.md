---
title: Tmux 简单配置
date: 2018-04-26
categories:
- vim
tags:
- tmux
- vim
---
Tmux 终端分屏利器。运行多个终端会话，你还可以通过 Tmux 使终端会话运行于后台或是按需接入、断开会话。实用高效
<!-- more -->

### 为什么配置

受不了<code>ctrl + b</code>（这两个组合键每次按的时候都要停顿一下...），还有<code>% "</code>分屏 -_-#

---
## 安装

[homebrew](https://brew.sh/index_zh-cn)安装
```shell
brew install tmux
```
## 配置

用户用户名<code>~</code>目录修改/新建<code>.tmux.conf</code>文件

我需要：
1. <code>c + b</code> 改成 稍微近一点到组合键（如：<code>c + a</code>）
2. <code>shift + % / "</code>分屏改成能理解到，我每次不记得**%** **"**哪个是垂直/水平
3. 支持鼠标点击选择

### .tmux.conf
```
# remap prefix from 'C-b' to 'C-a'
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix

# split panes using | and -
bind | split-window -h
bind - split-window -v
unbind '"'
unbind %

# Enable mouse mode (tmux 2.1 and above)
set -g mouse on
# Enable mouse mode (tmux previous 2.1)
set -g mode-mouse on
set -g mouse-resize-pane on
set -g mouse-select-pane on
set -g mouse-select-window on
```
> 查看tmux版本 <code>tmux -V</code>

> **注意：** 修改配置并使其生效 你修改了~/.tmux.conf, 但是并没有起作用。你退出tmux, 重新进去，发现还是没有生效。 
这是因为tmux后台有一个server, 在你第一次使用它时启动, 并创建会话。 当你退出时，它并没有退出。正确的方法杀掉server后再重新进入：
```shell
tmux kill-server

tmux
```
---
## 常用快捷键
默认命令前缀：<code>ctrl + b</code>（上面，我们默认改成了<code>ctrl + a</code>）
### 基本操作
|命令|说明|
|--|--|
|?|列出所有快捷键；按 q 返回|
|d|脱离当前会话,可暂时返回 Shell 界面|
|s|选择并切换会话；在同时开启了多个会话时使用|
|D|选择要脱离的会话；在同时开启了多个会话时使用|
|:|进入命令行模式；此时可输入支持的命令|
|[|复制模式，光标移动到复制内容位置，空格键开始，方向键选择复制，回车确认，q/Esc 退出|
|]|进入粘贴模式，粘贴之前复制的内容，按 q/Esc 退出|
|~|列出提示信息缓存；其中包含了之前 tmux 返回的各种提示信息|
|t|显示当前的时间|
### 单一窗格操作
|命令|说明|
|--|--|
|x|关闭当前分屏|
|!|将当前面板置于新窗口,即新建一个窗口,其中仅包含当前面板|
|q|显示面板编号|
|o|选择当前窗口中下一个面板|
|{|向前置换当前面板|
|}|向后置换当前面板|
|z|最大化当前所在面板|
|方向键|移动光标选择对应面板|
|alt+o|逆时针旋转当前窗口的面板|
|ctrl+o|顺时针旋转当前窗口的面板|
### 窗口面板操作
|命令|说明|
|--|--|
|c|创建新窗口|
|&|关闭当前窗口|
|[0-9]|数字键切换到指定窗口|
|p|切换至上一窗口|
|n|切换至下一窗口|
|l|前后窗口间互相切换|
|w|通过窗口列表切换窗口|
|,|重命名当前窗口，便于识别|
|.|修改当前窗口编号，相当于重新排序|
|f|在所有窗口中查找关键词，便于窗口多了切换|

> 参考：[Tmux 简介与使用](http://blog.konghy.cn/2016/09/29/tmux/)