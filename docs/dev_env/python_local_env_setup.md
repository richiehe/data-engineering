# Python本地虚拟环境搭建
在我们准备机器学习前，先把开发环境配好，这个比较至关重要，所谓磨刀不误砍柴工。

本篇内容针对MacOS用户，并且主要讲解python的虚拟环境的搭建。当然，可能有人问了，MacOS自带python环境，要python2有python2，要python3有python3，pip install直接安装各种依赖就好了啊，干啥要整个python虚拟环境呢？

当然了，你要是自己开发开发，随便玩儿玩儿，对python环境不怎么洁癖的话，用系统自带的就行。如果你开发过几个python项目，并且各个项目对python以及依赖包的版本要求不一的时候，你就会发现虚拟环境是个非常简单高效的方法，因为你可能会因为python对开发环境的污染非常恼怒😡。

所以此文章主要会讲以下几点：

针对python的虚拟环境：pyenv
主要针对python依赖包：pyenv-virtualen

## 准备工作
一些安装依赖于macOS上的Homebrew包管理工具，macOS神器之一，安装如下
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
> 如果你的系统中以前用其他方式安装过python, 可能存在不兼容的情况


## pyenv
pyenv主要是用来做python版本的控制，比如可以将python的全局版本切换至3.6，或者3.7等不同的几个版本

安装pyenv
```bash
brew update
brew install pyenv
```

加入环境变量，比如加到zshrc，或者bashrc, bash_profile下, 之后记得source一下
```
eval "$(pyenv init -)"
```

查询有哪些版本可用
```bash
pyenv install --list
```

安装某个版本的python，比如说安装3.6.8
```bash
pyenv install 3.6.8
```

列出系统中python的可用版本
```bash
pyenv versions
```

将系统中的python版本设置为某个版本，比如说设置成3.6.8
```bash
pyenv global 3.6.8
```

检查python版本
```bash
$ python --version
Python 3.6.8
```

## pyenv-virtualenv
pyenv-virtualenv其实就是pyenv的一个插件，用来管理python的各种虚拟环境，有了这个虚拟环境以后，再也不用担心pip install会污染以前安装过的python的依赖包了。

安装pyenv-virtualenv
```bash
brew install pyenv-virtualenv
```

添加环境变量, eval "$(pyenv virtualenv-init -)", 之后记得source一下
```bash
eval "$(pyenv virtualenv-init -)"
```

创建python虚拟环境
```bash
pyenv virtualenv 3.6.8 my-virtual-env
```
> 这个指令说明一下，3.6.8是你需要基于的python版本，这个python版本可以通过之前pyenv的指令进行安装，后面my-virtual-env是你创建这个虚拟环境的名称，以后需要根据这个名字进入这个虚拟环境


进入python虚拟环境
```bash
pyenv activate my-virtual-env
```

退出虚拟环境
```bash
pyenv deactivate
```

列出已有的虚拟环境
```bash
pyenv virtualenvs
```

删除虚拟环境
```bash
pyenv uninstall my-virtual-env
```

### Reference:
- [pyenv](https://github.com/pyenv/pyenv)
- [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)