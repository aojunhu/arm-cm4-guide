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
wget -c http://soft.vpser.net/lnmp/lnmp1.5.tar.gz && tar zxf lnmp1.5.tar.gz && cd lnmp1.5 && ./install.sh lnmp
```
����������ִ�к󣬻����������ʾ��ѡ�����ݿ�汾������Ĭ�ϣ�ֱ�ӻس�����
��Ҫ�������ݿ�MySQL��root���루������ֱ�ӻس���������Ϊroot������ס���룡��������Ҫ�á�

ȷ���Ƿ�����MySQL InnoDB�������ȷ���Ƿ����ÿ������� y ������ y ��ʾ���ã����� n ��ʾ�����á�Ĭ��Ϊy ���ã������س�������һ����ѡ��MySQL�汾��֮����һ����ѡ��PHP�汾��
֮��ѡ���Ƿ�װ�ڴ��Ż���
��ʾ��Press any key to install��or Press Ctrl+c to cancel���󣬰��س���ȷ�Ͽ�ʼ��װ��LNMP�ű��ͻ��Զ���װ����Nginx��MySQL��PHP��phpMyAdmin��Zend Optimizer�⼸�������
��װʱ����ܻἸʮ���ӵ�����Сʱ���ȣ���Ҫ�ǻ������������ٵ�ԭ������Ӱ�졣

֮��ȴ���װ��ɡ�

## 3.3 �����������
��������Ĳ������Ѿ���װ�����վ�����л���LNMP����������Ҫ�����������������վ���������������Ĺ�����һ������ʽ��ҳ�档
```
lnmp vhost add

Please enter domain(example: www.lnmp.org): www.smusicc.com
 Your domain: www.smusicc.com
Enter more domain name(example: lnmp.org *.lnmp.org): smusicc.com
 domain list: smusicc.com
Please enter the directory for the domain: www.smusicc.com
Default directory: /home/wwwroot/www.smusicc.com:
Virtual Host Directory: /home/wwwroot/www.smusicc.com
Allow Rewrite rule? (y/n) y
Please enter the rewrite of programme,
wordpress,discuz,typecho,sablog,typecho rewrite was exist.
(Default rewrite: other): wordpress
You choose rewrite: wordpress
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

��������1.5���������SSL����
```
Add SSL Certificate (y/n) n
```
��ʾ Press any key to start create virtul host�� �󣬻س�ȷ�ϱ�Ὺʼ��������������
��ӳɹ�����ʾ��ӵ�������Ŀ¼��α��̬����־�����ݿ⡢FTP�������Ϣ��
��Ȼ������ĸ��������ǿ���ͨ���޸������ļ����и����ġ�����û��Ҫ̫���ᡣͨ��vi�޸Ļ������ص������޸Ķ����ԡ��������������ļ��ڣ�
```
vi /usr/local/nginx/conf/vhost/����.conf
```
## 3.4 ���FTP server
```
# cd ~/lnmp1.5/
# ./pureftpd.sh

# lnmp ftp add
```
ftp account name:   ftp_admin
password for ftp account: nxxx1
directory for ftp account: /home/wwwroot


## 3.5 WordPress�İ�װ
˵�ǰ�װ��������˵�ǰ�WordPressѹ������ѹ���ٰ��������ݶ��ƶ�����������Ŀ¼�¶��ѣ�����Ķ���һЩ�������ֱ�Ӹ���ִ�оͿ��ԡ�
### 3.5.1 WordPress�ļ��Ĳ���
��ʹ��cd�������������Ŀ¼�£�ע�⣺�滻�����Լ�������Ŀ¼����
```
cd /home/wwwroot/www.smusicc.com
wget https://cn.wordpress.org/wordpress-4.9.4-zh_CN.tar.gz
tar -zxvf wordpress-4.9.4-zh_CN.tar.gz
mv wordpress/* .
rm -rf wordpress
```
**ע��**������Ҫ��һЩ�������ã�
+ �޸�Ŀ¼ /home/wwwroot��Ȩ��
��ΪWordPress���ز������Ҫʹ��ftp�û����û���Ϊwww����/home/wwwroot��ownerΪroot��
```
#chattr -i /home/wwwroot/default/.user.ini 
# chattr -i /home/wwwroot/www.firstdecors.com/.user.ini 
# chown -R www:www /home/wwwroot/
# chattr +i /home/wwwroot/default/.user.ini 
# chattr +i /home/wwwroot/www.firstdecors.com/.user.ini
```
### 3.5.2 WordPress�İ�װ
�����ʱ��һ����˵�����Ѿ���������ˣ���ʱ��ֻҪ������������������������ֱ�ӿ���WordPress�İ�װ�����ˡ�
�����ʼ����������֮ǰ�����ݿ��������ݿ��û��������루������Ĭ�ϣ���
֮����ʾ�Ƿ�����ȷ�������ݿ⣬�������İ�װ��

վ����⣺ First Decoration Materials Co., Ltd
�û����� adxxxxin
���룺 3t4CXeQVPHoDkl&msT
���ĵ����ʼ��� hxxxn@126.com

�����̨��http://www.firstdecors.com/wp-admin/