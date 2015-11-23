title: macbook删除win7系统后无法合并分区的解决办法
tags: [macbook, win7, 双系统, 合并分区]
date: 2015-10-30

----

这个问题算是存在已久的一个问题了。网上一搜也会有各式各样的答案。这里提供一个比较全的帖子：[http://jingyan.baidu.com/article/0eb457e50877d303f1a90531.html](http://jingyan.baidu.com/article/0eb457e50877d303f1a90531.html)

但是，经过测试，上面的文章提到的办法还是不能解决我的问题。



我是通过以下的办法来解决的：
	
	<font size="6px" color="#ff0000">打开终端，输入sudo -s回车，输入密码回车，输入 diskutil cs revert / 回车，重启后再打开磁盘工具分区图右下角就可以往下拉了～</font>
	
