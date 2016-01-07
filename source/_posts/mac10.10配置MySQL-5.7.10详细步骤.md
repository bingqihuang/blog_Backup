title: mac10.10配置MySQL-5.7.10详细步骤
tags: [mac,mysql, mysql5.7.10]
date: 2016-01-07

---

  新的一年里，首先祝福大家，祝福自己，在2016收获满满！
  
## 问题

**mysql-5.7.x的版本和旧的版本差别还是很大的。安装的时候会生成一个临时密码，一不小心，就忘了记下这个密码了。以下是详细的安装教程。**

## 安装mysql-5.7.x详细步骤


* 到官网下载最新的mysql mysql-5.7.10-osx10.10-x86_64.dmg。

	下载链接：[http://dev.mysql.com/downloads/mysql/](http://dev.mysql.com/downloads/mysql/)

* 安装好mysql

	安装时会弹出一个弹窗，
	
	<font size="5px" color="#ff0000">里面有root账号的临时密码，这个要记下来！后面会用到。</font>
	
		例如：nynKvqibL3;a

* 在偏好设置里，找到mysql，启动mysql

* 设置命令搜索路径
	打开终端，输入：
	* sudo vi ~/.bash_profile
	* 按“i”键，进入编辑模式
	* 粘贴以下内容
	
	```bash
	# mysql
	alias mysql='/usr/local/mysql/bin/mysql'
	alias mysqladmin='/usr/local/mysql/bin/mysqladmin'
	# ls

	alias ls='ls -G'
	```
	
	* 按esc键，退出编辑模式
	* 输入 ":wq",保存文件,重启终端程序

* 输入临时密码，设置新密码
	* 在终端输入指令：$ mysqladmin -u root -p password
	* 输入临时密码： nynKvqibL3;a
	* 输入新密码：*******
	* 确认新密码：*******

	***接下来会出现一个提示：Since password will be sent to server in plain text, use ssl connection to ensure password safety.
	无视之。***

* 退出终端，重新登录mysql 

```bash 
 mysql -u root -p
```
	
* 输入刚才设置的新密码

* ending。

