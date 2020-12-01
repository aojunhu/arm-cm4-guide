搭建一个网站需要三个必备的因素，即：**域名**、**服务器**、**程序**。
# 1.域名
使用godaddy(www.godaddy.com)。国外的域名注册商都是不限制解析数目的。而且Godaddy是支持支付宝付款的。
+ Create an account and login.
+ Buy a domain name.
+ Go to **My Account** --> **My Products**
+ Click **DNS** button of the domain.
+ Set **A**'s Value to **your_server_ip**
# 2.服务器
经过对比筛选，选择Vultr，原因不解释。
Vultr： https://www.vultr.com/
+ Create an account and login.
+ Buy a host space.
+ Deploy New Server.
select **Server Location**, **Server Type**, **Server Size**, **Additional Features** and etc.
+ In **Servers** --> **Instances**, your server will be here, and click **...** --> **Server Details**
Write down the **IP Address**, **Username** and **Password**

# 3.建站

## 3.1 安装&配置Xshell
+ Download an install xshell in your windows pc.
+ run xshell and go to **文件** --> **新建** --> **连接**
设置 连接名称、主机IP、端口号、身份验证信息，然后登录Vultr VPS。

## 3.2 安装LNMP环境

```
$ wget -c http://soft.vpser.net/lnmp/lnmp1.6.tar.gz
$ tar -zxvf lnmp1.6.tar.gz
$ cd lnmp1.6
$ sudo ./install.sh
```
按上述命令执行后，会出现如下提示：选择数据库版本（建议默认，直接回车）。
需要设置数据库MySQL的root密码（不输入直接回车将会设置为root），记住密码！！！后面要用。
```
Please setup root password of MySQL.
Please enter: nxx1
```
确认是否启用MySQL InnoDB，如果不确定是否启用可以输入 y ，输入 y 表示启用，输入 n 表示不启用。默认为y 启用，输入后回车进入下一步，选择MySQL版本。之后下一步，选择PHP版本。
```
Do you want to enable or disable the InnoDB Storage Engine?
Default enable,Enter your choice [Y/n]: Y
You will enable the InnoDB Storage Engine
===========================
You have 9 options for your PHP install.
1: Install PHP 5.2.17
2: Install PHP 5.3.29
3: Install PHP 5.4.45
4: Install PHP 5.5.38
5: Install PHP 5.6.40 (Default)
6: Install PHP 7.0.33
7: Install PHP 7.1.30
8: Install PHP 7.2.19
9: Install PHP 7.3.6
Enter your choice (1, 2, 3, 4, 5, 6, 7, 8 or 9): 
No input,You will install PHP 5.6.40
===========================
You have 3 options for your Memory Allocator install.
1: Don't install Memory Allocator. (Default)
2: Install Jemalloc
3: Install TCMalloc
Enter your choice (1, 2 or 3): 
No input,You will not install Memory Allocator.

Press any key to install...or Press Ctrl+c to cancel
```
之后选择是否安装内存优化。
提示”Press any key to install…or Press Ctrl+c to cancel“后，按回车键确认开始安装。LNMP脚本就会自动安装编译Nginx、MySQL、PHP、phpMyAdmin、Zend Optimizer这几个软件。
安装时间可能会几十分钟到几个小时不等，主要是机器的配置网速等原因会造成影响。

之后等待安装完成。


在安装WordPress之前，建议安装PHP缓存加速类扩展，对降低VPS压力和提高WordPress速度大有裨益。推荐安装两个：OPcache和Memcached。
+ 安装OPcache
```
$ cd lnmp1.6/
$ sudo ./addons.sh install opcache
```
+ 安装Memcached
```
$ sudo ./addons.sh install memcached
```

## 3.3 添加虚拟主机
经过上面的操作，已经安装完成网站的运行环境LNMP，接下来需要创建虚拟主机添加网站，创建虚拟主机的过程是一个交互式的页面。
```
$ sudo lnmp vhost add

Please enter domain(example: www.lnmp.org): www.firstdecors.com
 Your domain: www.firstdecors.com
Enter more domain name(example: lnmp.org *.lnmp.org): firstdecors.com
 domain list: firstdecors.com
Please enter the directory for the domain: www.firstdecors.com
Default directory: /home/wwwroot/www.firstdecors.com:
Virtual Host Directory: /home/wwwroot/www.firstdecors.com
Allow Rewrite rule? (y/n) y
Please enter the rewrite of programme,
wordpress,discuz,typecho,sablog,typecho rewrite was exist.
(Default rewrite: other): wordpress
You choose rewrite: wordpress
Enable PHP Pathinfo? (y/n) n
Disable pathinfo.
Allow access log? (y/n) n
Disable access log.
```
再接下来就是创建数据库，这里如果要创建的话，会创建成一个用户名和数据库名相同的。
```
Create database and MySQL user with same name (y/n) y
Enter current root password of Database (Password will not shown):
```
如果选择y的话，会要先验证MySQL的root密码（上面设置好的 – 密码不显示，输入就好了，按回车）
验证后会让你输入数据库名，回车后会提示你，已经创建了一个和数据库名相同的用户名。然后就是输入数据库密码。
```
Enter database name: firstdecors
Your will create a database and MySQL user with same name: firstdecors
Please enter password for mysql user firstdecors: nxx1
Your password: nxx1 
Create ftp account (y/n) y
Enter ftp account name: firstdecors
Enter password for ftp account firstdecors: nxx1
```

接下来是1.5新增的添加SSL功能
```
Add SSL Certificate (y/n) n
```
提示 Press any key to start create virtul host… 后，回车确认便会开始创建虚拟主机。
添加成功会提示添加的域名、目录、伪静态、日志、数据库、FTP等相关信息。
```
================================================
Virtualhost infomation:
Your domain: www.firstdecors.com
Home Directory: /home/wwwroot/www.firstdecors.com
Rewrite: wordpress
Enable log: no
Database username: firstdecors
Database userpassword: nxx1
Database Name: firstdecors
FTP account name: firstdecors
FTP account password: nxx1
================================================
```
当然，这里的各项配置是可以通过修改配置文件进行更正的。所以没必要太纠结。通过vi修改或者下载到本地修改都可以。虚拟主机配置文件在：
```
vi /usr/local/nginx/conf/vhost/www.firstdecors.com.conf
```


**重要提示**：
1. 安装完后，默认server root为/home/wwwroot/default，需要改成新添加的vhost。
```
$ sudo vi /usr/local/nginx/conf/nginx.conf
server
	{
        root  /home/wwwroot/default;  
        ---> 
        root  /home/wwwroot/www.firstdecors.com;
	}

$ sudo /usr/local/nginx/sbin/nginx -s reload
```

2. 删除/home/wwwroot/default中除phpmyadmin和.user.ini之外的其余文件。并把phpmyadmin重命名为不易猜到的名称。
```
$ cd /home/wwwroot/default
$ sudo rm index.html lnmp.gif p.php phpinfo.php
$ sudo mv phpmyadmin xxxx
```

## 3.4 添加FTP server
```
$ cd ~/lnmp1.5/
$ sudo ./pureftpd.sh

#If not add before.
$ sudo lnmp ftp add
```
ftp account name:   firstdecors
password for ftp account: nxxx1
directory for ftp account: /home/wwwroot


## 3.5 WordPress的安装
说是安装，倒不如说是把WordPress压缩包解压后，再把里面内容都移动到到域名的目录下而已，这里的都已一些基本命令，直接复制执行就可以。
### 3.5.1 WordPress文件的部署
先使用cd命令进入域名的目录下（注意：替换成你自己的域名目录）：
```
cd /home/wwwroot/www.firstdecors.com
$ sudo wget https://cn.wordpress.org/wordpress-5.2.2-zh_CN.tar.gz
$ sudo tar -zxvf wordpress-5.2.2-zh_CN.tar.gz
$ sudo mv wordpress/* .
$ sudo rm -rf wordpress
```
**注意，还需要做一些额外设置**：
+ 修改目录 /home/wwwroot的权限
因为WordPress下载插件，需要使用ftp用户，用户组为www，而/home/wwwroot的owner为root。
```
$ sudo chattr -i /home/wwwroot/default/.user.ini 
$ sudo chattr -i /home/wwwroot/www.firstdecors.com/.user.ini 
$ sudo chown -R www:www /home/wwwroot/
$ sudo chattr +i /home/wwwroot/default/.user.ini 
$ sudo chattr +i /home/wwwroot/www.firstdecors.com/.user.ini
```
### 3.5.2 WordPress的安装
到这个时候，一般来说域名已经解析完毕了，这时候只要在浏览器输入你的域名，就能直接看到WordPress的安装界面了。
点击开始后，依次输入之前的数据库名，数据库用户名和密码（后两项默认）。
之后，提示是否能正确连接数据库，进行最后的安装。

站点标题： First Decoration Materials Co., Ltd
用户名： admin
密码： nxx1
您的电子邮件： hxxxn@126.com


管理后台：http://IP/wp-admin/ or http://IP/wp-login.php
