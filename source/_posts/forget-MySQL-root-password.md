---
title: 重置MySQL的root密码
date: 2017-03-01 16:14:21
tags:
        - MySQL
---

> 经历过一次在Mac上装MySQL的过程，就觉得MySQL真坑，提示的一次性密码居然也是错的。。果断开始查如何重置MySQL root密码。。

*  停止 mysql server.  通常是在 '系统偏好设置' > MySQL > 'Stop MySQL Server'

* 打开你的iTerm ，输入

```
          sudo /usr/local/mysql/bin/mysqld_safe --skip-grant-tables
```

   
* 再开一个iTerm窗口吧，上一个窗口不要关，新的iTerm终端输入：


```

sudo /usr/local/mysql/bin/mysql -u root

//敲完密码已经进入到MySQL的命令行终端了，紧接着继续

UPDATE mysql.user SET authentication_string=PASSWORD('这里写你要设置的密码') WHERE User='root';

// root 可更改，你想重置那个用户就写哪个

FLUSH PRIVILEGES;

//退出
quit;

```

如果不出意外，估计就可以啦。
尝试用`mysql -u root -p`登录吧

如果登录了以后使用语句依旧报错，类似于`ERROR 1820 (HY000): You must reset your password using ALTER USER statement before executing this statement` 使用 `SET PASSWORD = PASSWORD('新密码');`
这样再尝试一下`show database;`语句，不报错就可以正常使用咯

