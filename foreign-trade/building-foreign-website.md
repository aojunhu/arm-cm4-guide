�һ����վ��Ҫ�����ر������أ�����**����**��**������**��**����**��
# 1.����
ʹ��godaddy(www.godaddy.com)�����������ע���̶��ǲ����ƽ�����Ŀ�ġ�����Godaddy��֧��֧��������ġ�
+ Create an account and login.
+ Buy a domain name.
+ Go to **My Account** --> **My Products**
+ Click **DNS** button of the domain.
+ Set **A**'s Value to **your_server_ip**
# 2.������
�����Ա�ɸѡ��ѡ��Vultr��ԭ�򲻽��͡�
Vultr�� https://www.vultr.com/
+ Create an account and login.
+ Buy a host space.
+ Deploy New Server.
select **Server Location**, **Server Type**, **Server Size**, **Additional Features** and etc.
+ In **Servers** --> **Instances**, your server will be here, and click **...** --> **Server Details**
Write down the **IP Address**, **Username** and **Password**

# 3.��վ

## 3.1 ��װ&����Xshell
+ Download an install xshell in your windows pc.
+ run xshell and go to **�ļ�** --> **�½�** --> **����**
���� �������ơ�����IP���˿ںš������֤��Ϣ��Ȼ���¼Vultr VPS��

## 3.2 ��װLNMP����

```
$ wget -c http://soft.vpser.net/lnmp/lnmp1.6.tar.gz
$ tar -zxvf lnmp1.6.tar.gz
$ cd lnmp1.6
$ sudo ./install.sh
```
����������ִ�к󣬻����������ʾ��ѡ�����ݿ�汾������Ĭ�ϣ�ֱ�ӻس�����
��Ҫ�������ݿ�MySQL��root���루������ֱ�ӻس���������Ϊroot������ס���룡��������Ҫ�á�
```
Please setup root password of MySQL.
Please enter: nxx1
```
ȷ���Ƿ�����MySQL InnoDB�������ȷ���Ƿ����ÿ������� y ������ y ��ʾ���ã����� n ��ʾ�����á�Ĭ��Ϊy ���ã������س�������һ����ѡ��MySQL�汾��֮����һ����ѡ��PHP�汾��
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
֮��ѡ���Ƿ�װ�ڴ��Ż���
��ʾ��Press any key to install��or Press Ctrl+c to cancel���󣬰��س���ȷ�Ͽ�ʼ��װ��LNMP�ű��ͻ��Զ���װ����Nginx��MySQL��PHP��phpMyAdmin��Zend Optimizer�⼸�������
��װʱ����ܻἸʮ���ӵ�����Сʱ���ȣ���Ҫ�ǻ������������ٵ�ԭ������Ӱ�졣

֮��ȴ���װ��ɡ�


�ڰ�װWordPress֮ǰ�����鰲װPHP�����������չ���Խ���VPSѹ�������WordPress�ٶȴ������档�Ƽ���װ������OPcache��Memcached��
+ ��װOPcache
```
$ cd lnmp1.6/
$ sudo ./addons.sh install opcache
```
+ ��װMemcached
```
$ sudo ./addons.sh install memcached
```

## 3.3 �����������
��������Ĳ������Ѿ���װ�����վ�����л���LNMP����������Ҫ�����������������վ���������������Ĺ�����һ������ʽ��ҳ�档
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
�ٽ��������Ǵ������ݿ⣬�������Ҫ�����Ļ����ᴴ����һ���û��������ݿ�����ͬ�ġ�
```
Create database and MySQL user with same name (y/n) y
Enter current root password of Database (Password will not shown):
```
���ѡ��y�Ļ�����Ҫ����֤MySQL��root���루�������úõ� �C ���벻��ʾ������ͺ��ˣ����س���
��֤��������������ݿ������س������ʾ�㣬�Ѿ�������һ�������ݿ�����ͬ���û�����Ȼ������������ݿ����롣
```
Enter database name: firstdecors
Your will create a database and MySQL user with same name: firstdecors
Please enter password for mysql user firstdecors: nxx1
Your password: nxx1 
Create ftp account (y/n) y
Enter ftp account name: firstdecors
Enter password for ftp account firstdecors: nxx1
```

��������1.5���������SSL����
```
Add SSL Certificate (y/n) n
```
��ʾ Press any key to start create virtul host�� �󣬻س�ȷ�ϱ�Ὺʼ��������������
��ӳɹ�����ʾ��ӵ�������Ŀ¼��α��̬����־�����ݿ⡢FTP�������Ϣ��
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
��Ȼ������ĸ��������ǿ���ͨ���޸������ļ����и����ġ�����û��Ҫ̫���ᡣͨ��vi�޸Ļ������ص������޸Ķ����ԡ��������������ļ��ڣ�
```
vi /usr/local/nginx/conf/vhost/www.firstdecors.com.conf
```


**��Ҫ��ʾ**��
1. ��װ���Ĭ��server rootΪ/home/wwwroot/default����Ҫ�ĳ�����ӵ�vhost��
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

2. ɾ��/home/wwwroot/default�г�phpmyadmin��.user.ini֮��������ļ�������phpmyadmin������Ϊ���ײµ������ơ�
```
$ cd /home/wwwroot/default
$ sudo rm index.html lnmp.gif p.php phpinfo.php
$ sudo mv phpmyadmin xxxx
```

## 3.4 ���FTP server
```
$ cd ~/lnmp1.5/
$ sudo ./pureftpd.sh

#If not add before.
$ sudo lnmp ftp add
```
ftp account name:   firstdecors
password for ftp account: nxxx1
directory for ftp account: /home/wwwroot


## 3.5 WordPress�İ�װ
˵�ǰ�װ��������˵�ǰ�WordPressѹ������ѹ���ٰ��������ݶ��ƶ�����������Ŀ¼�¶��ѣ�����Ķ���һЩ�������ֱ�Ӹ���ִ�оͿ��ԡ�
### 3.5.1 WordPress�ļ��Ĳ���
��ʹ��cd�������������Ŀ¼�£�ע�⣺�滻�����Լ�������Ŀ¼����
```
cd /home/wwwroot/www.firstdecors.com
$ sudo wget https://cn.wordpress.org/wordpress-5.2.2-zh_CN.tar.gz
$ sudo tar -zxvf wordpress-5.2.2-zh_CN.tar.gz
$ sudo mv wordpress/* .
$ sudo rm -rf wordpress
```
**ע�⣬����Ҫ��һЩ��������**��
+ �޸�Ŀ¼ /home/wwwroot��Ȩ��
��ΪWordPress���ز������Ҫʹ��ftp�û����û���Ϊwww����/home/wwwroot��ownerΪroot��
```
$ sudo chattr -i /home/wwwroot/default/.user.ini 
$ sudo chattr -i /home/wwwroot/www.firstdecors.com/.user.ini 
$ sudo chown -R www:www /home/wwwroot/
$ sudo chattr +i /home/wwwroot/default/.user.ini 
$ sudo chattr +i /home/wwwroot/www.firstdecors.com/.user.ini
```
### 3.5.2 WordPress�İ�װ
�����ʱ��һ����˵�����Ѿ���������ˣ���ʱ��ֻҪ������������������������ֱ�ӿ���WordPress�İ�װ�����ˡ�
�����ʼ����������֮ǰ�����ݿ��������ݿ��û��������루������Ĭ�ϣ���
֮����ʾ�Ƿ�����ȷ�������ݿ⣬�������İ�װ��

վ����⣺ First Decoration Materials Co., Ltd
�û����� admin
���룺 nxx1
���ĵ����ʼ��� hxxxn@126.com


�����̨��http://IP/wp-admin/ or http://IP/wp-login.php
