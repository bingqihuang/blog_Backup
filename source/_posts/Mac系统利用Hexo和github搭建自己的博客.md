title: 新博客-记录下折腾此博客的过程！
tags: [mac, Hexo, 博客]
date: 2015-07-31 10:00:00

---

很高兴自己动手成功搭建了该博客。虽然在Mac上操作省了不少步骤，过程挺简单，但是还是需要天时地利人和（好吧，有些夸张）。
第一篇博客就用来记录搭建博客的过程吧---Mac系统利用Hexo和github搭建自己的博客

## 环境和工具准备

Mac系统上使用homebrew套件来安装一些工具非常方便。

### 1.安装Homebrew

``` bash
$ ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```

#### Homebrew常用指令

指令 				 | 用途 
---------------------|----------------------
$ brew install [xxx] | 安装套件  
$ brew remove [xxx]  | 移除套件  
$ brew outdated 	 | 列出已安装套件中可更新的  
$ brew upgrade 		 | 更新所有套件
$ brew upgrade [xxx] | 更新指定套件
$ brew search 		 | 显示所有可安装的套件
$ brew search [xxx]  | 搜索套件


### 2.git安装和github注册

#### 2.1 git安装
``` bash
$ brew install git
```

#### 2.2 github 注册和仓库的创建

注册流程(略).

特别注意：仓库创建在右上角，仓库名要设置为：你的github username.github.io.

### 3.Node.js安装

``` bash
$ brew install node 
```

检验是否安装成功,
``` bash
$ node -v
$ npm -v
```

## Hexo 安装

``` bash
$ npm install -g hexo   # -g表示全局安装，如果去掉，npm将默认在当前项目安装
```
安装hexo的过程遇到了问题。老是报错。log显示多次hexo-gyp rebuild 都不成功，安装一些东西失败，导致到最后hexo generate 和 hexo deploy时失败。
![hexo_fail01](/img/hexo_generate_fail.png) 
![hexo_fail02](/img/hexo_deploy_fail.png) 

如果出现以上错误，得卸载已经安装的hexo,
``` bash
$ npm uninstall -g hexo 
```

解决方案：
	网上查了好久，包括更换npm的镜像源为国内的，也解决不了。最终解决问题的做法是：安装 [Command Line Tools](http://railsapps.github.io/xcode-command-line-tools.html)

简单粗暴，直接在终端执行命令：
``` bash
$ xcode-select --install 
```
已经安装Xcode的朋友别大意，很可能你在安装Xcode的时候并没有安装Command Line Tools。
至此，你再重新安装hexo，很可能就跟我一样，完美安装了！

### 1.Hexo操作

进入要操作的目录，比如我的是：Documents/hexo-blog,
``` bash
$ hexo init
$ hexo generate # 可简写：hexo g
$ npm install # 初始化依赖
$ hexo server # 可简写：hexo s, 启动服务器
```

到这儿，你就可以根据终端提示的地址访问你的本地博客啦！

### 2.将本地博客推送到github上

首先，需要安装部署器,输入运行命令行：
``` bash
npm install hexo-deployer-git --save
```

其次，打开博客目录下地_config.yml,翻到最后（翻页：ctrl+d），设置如下：
![hexo-deploy-setup](/img/hexo-deploy-setup.png) 

## 总结

很惊讶，没接触过markdown的我就直接上手写了这篇文章！
所以说，人的潜力是无穷的，不逼自己一把，你也不知道你的极限到底在哪儿！
