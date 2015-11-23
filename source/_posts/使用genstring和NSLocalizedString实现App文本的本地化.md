title: 使用genstring和NSLocalizedString实现App文本的本地化
tags: [genstring, iOS开发, 本地化]
date:2015-08-28

iOS提供了简便的方法来实现本地化，其中用的最多的就是NSLocalizedString。
首先查看下NSLocalizedString是什么：

## NSLocalizedString简介
``` bash
#define NSLocalizedString(key,comment)

[[NSBundle mainBundle]localizedStringForKey:(key) value:@"" table:nil];

```
这是一个宏，本质上调用了函数localizedStringForKey:这样，这个宏做的其实就是在当前bundle中查找资源文件名Localizable.strings中键值key所指向的字符串，这样就不难理解还有诸如：NSLocalizedStringFromTable的宏了。

### 举栗子

在不考虑本地化的情况下，外面如果在代码中给一个Button定义title，一般会这样写：

```bash
1 button.titleLabel.text = @"btn_title";
```

当虚考虑本地化的问题时，把要显示给用户看的字符串做如下修改：（对于内部使用的字符串就用不着本地化了）
```bash
1
button.titileLabel.text = NSLocalizedString(@"btn_title",@"按钮title");
```

NSLocalizedString是一个定义在NSBundle.h中的宏，用途是寻找当前系统语言对应的Localizable.strings文件中的某个key的值。
第一个参数是key的名字，第二个参数是对这个“键值对”的注释，在用genstrings工具生成Loclizable.strings文件时会自动加上去。
到目前为止，外面还没有生成Localizable.strings文件，这个一个逆向的过程，也就是先写好调用过程，再生成strings资源文件。

### 利用genstrings工具

当外面把所有的.m文件都修改好以后，就该genstring工具了。

* 启动终端，进入工程所在的目录.
* 新建两个目录，推荐放在资源目录下

>目录名会作用到Localizable.strings文件对应的语言，不能写错了。这里zh-Hans指简体中文，注意不能用zh.lproj表示。

```bash
1 mkdir zh-Hans.lproj
2 mkdir en.lproj
```
* 生成Localizable.strings文件

```bash
1 genstrings -o zh-Hans.lproj *.m
2 genstrings -o en.lproj *.m
```
> -o<文件夹>，指定生成的Localizable.strings文件放置的目录
*.m，扫描所有的.m文件，这里支持的文件还包括.h,.java等.

* 右键点击工程的Resources目录，选择“New group”,添加两个目录zh-Hans.lproj和en.lproj
* 在新建的group中添加刚刚生成的Loclizable.strings文件.
* 最后在Localizable.strings文件中，修改每个key所对应的内容，就可以了。

代码已经上传github，[地址在这](https://github.com/bingqihuang/BQLocalizableStringExample).

## 总结

1.在代码里用NSLocalizedString获取要本地化的字符串.

2.用genstrings扫描代码文件，生成Localizable.strings,然后加到工程中。
