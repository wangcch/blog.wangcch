---
title: 添加VS Code命令行
date: 2018-02-25
categories:
- other
tags:
- vs code
---

习惯用atom的都知道，可以在文件目录中启动atom，非常方便。使用vs却发现没有。网上搜索配置<code>.bash_profile</code>，然而我没有这个文件，手动添加后可以使用，但是终端重启后又回失效。

<!-- more -->

最后在官网找到了方法（默认不开启）
[https://code.visualstudio.com/docs/setup/](https://code.visualstudio.com/docs/setup/)
## 自动配置
1. 打开VS Code 
2. 打开Command Palette(cmd+shift+p) 输入<code>shell command</code>
3. 选择 <code>Install 'code' command in PATH</code>
4. 重启终端

现在你可以使用<code>code </code>命令来打开文件夹了
> 注意：如果您的早期VS代码版本（或等效版本）中仍旧存在旧code别名.bash_profile，请将其删除并通过执行命令行命令：PATH命令中的安装'code'命令来替换它。

## 手动配置
```
cat << EOF >> ~/.bash_profile
# Add Visual Studio Code (code)
export PATH="\$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"
EOF

```