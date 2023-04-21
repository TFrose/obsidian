# 一. Linux服务器安装

**安装Linux**[**服务器**](https://cloud.tencent.com/product/cvm?from=10680)**可选择：Centos，Redhat，Oracle Linux。** 
**本文配置为 `Redhat 7.9 x86_64`，`内存2G`，`硬盘50G`。**

![](https://ask.qcloudimg.com/http-save/yehe-3615093/68d5315452ac97b13e526a117b78e547.png?imageView2/2/w/1620)

![](https://ask.qcloudimg.com/http-save/yehe-3615093/297cac8e5c0b3e5c304fea08d51e56b3.png?imageView2/2/w/1620)
# 二. mysql安装介质下载

**官网下载地址：**[**MySQL Product Archives**](https://downloads.mysql.com/archives/community/)
-   选择版本：经典版5.7.20 linux-Generic x86-64

![](https://ask.qcloudimg.com/http-save/yehe-3615093/c088bf9d2a477113eacd6f4d58b46b10.png?imageView2/2/w/1620)

下载完之后，安装包如下：`mysql-5.7.20-linux-glibc2.12-x86_64.tar.gz`，通过ftp工具上传至Linux服务器文件夹下。

# 三. mysql安装
**以上准备工作已经做完了，现在连接Linux主机：`ssh root@10.211.55.200`**

## 1 检查安装介质
![](https://ask.qcloudimg.com/http-save/yehe-3615093/4f7069dd2cd9c0be567caaacc779e138.png?imageView2/2/w/1620)

## 2 解压安装介质
```javascript
cd /soft
tar -xvf mysql-5.7.20-linux-glibc2.12-x86_64.tar.gz
##将解压出的文件夹名称修改为mysql：
mv mysql-5.7.20-linux-glibc2.12-x86_64 mysql
```

复制
![](https://ask.qcloudimg.com/http-save/yehe-3615093/283361580179ec084759a4b42efc3fcf.png?imageView2/2/w/1620)

![](https://ask.qcloudimg.com/http-save/yehe-3615093/ae1f8e1285d2693580cfca69ab86014b.png?imageView2/2/w/1620)

## 3 建立用户和组

```javascript
groupadd mysql
useradd -r -g mysql -s /bin/false mysql
```

复制

![](https://ask.qcloudimg.com/http-save/yehe-3615093/70cf569856fe0b4788589a92b300ec13.png?imageView2/2/w/1620)

## 4 创建相关目录

```javascript
mkdir -p /data/mysql
chown -R mysql:mysql /data
chown -R mysql:mysql /soft
chmod 750 /data
```

复制
![](https://ask.qcloudimg.com/http-save/yehe-3615093/9ec3a1c0aa7d55343c23874bd3de5e16.png?imageView2/2/w/1620)

## 5 配置环境变量
```javascript
cat <<EOF>> /root/.bash_profile
export PATH=\$PATH:/soft/mysql/bin
EOF
##生效环境变量
source /root/.bash_profile
```

复制
![](https://ask.qcloudimg.com/http-save/yehe-3615093/3977e934e9de528cdab0d7eb59aca57f.png?imageView2/2/w/1620)

## 6 安装依赖包

```javascript
##挂载镜像源
mount /dev/cdrom /mnt
##配置yum源
cat <<EOF>>/etc/yum.repos.d/local.repo
[local]
name=local
baseurl=file:///mnt
gpgcheck=0
enabled=1
EOF
##安装依赖包
yum install -y libaio
```

复制
![](https://ask.qcloudimg.com/http-save/yehe-3615093/1be7f122e95afe97db58bdbd6f90ed04.png?imageView2/2/w/1620)

## 7 卸载自带mariadb和mysql
-   检查系统是否安装mysql：`rpm -qa | grep mysql`，因为我是最小化安装所以没有。
-   如果有则强制卸载：`rpm -e --nodeps $(rpm -qa | grep mysql)`

![](https://ask.qcloudimg.com/http-save/yehe-3615093/cb87076a90625ae9e297354b3fed0b18.png?imageView2/2/w/1620)

-   检查系统是否安装mariadb：`rpm -qa | grep mariadb`
-   如果有则强制卸载：`rpm -e --nodeps $(rpm -qa | grep mariadb)`，这里卸载成功。

![](https://ask.qcloudimg.com/http-save/yehe-3615093/53caab4828409a17bfba9ee0fcd3b182.png?imageView2/2/w/1620)

# 四. mysql初始化
-   **通过以下命令初始化创建mysql数据库：**

```javascript
mysqld --initialize --user=mysql --basedir=/soft/mysql --datadir=/data/mysql/
```

复制
参数： `--basedir` 为mysql解压目录，`--datadir` 为mysql数据存放目录。
![](https://ask.qcloudimg.com/http-save/yehe-3615093/eeeb95cecd4738a8c57edba782e71e56.png?imageView2/2/w/1620)

**注意：这里框出的是root用户的初始密码：`yhfvt_rP,24M`**

-   **配置my.cnf文件**

```javascript
cat <<EOF>/etc/my.cnf
[mysqld]
user=mysql
basedir=/soft/mysql
datadir=/data/mysql
server_id=6
port=3306
socket=/tmp/mysql.sock
##客户端
[mysql]
socket=/tmp/mysql.sock
prompt=lucifer [\\\\d]>
EOF
```

复制

![](https://ask.qcloudimg.com/http-save/yehe-3615093/fe4f4ece8e33e77d5a454b04d606fc0f.png?imageView2/2/w/1620)

-   **启动mysql服务：**
```javascript
/soft/mysql/support-files/mysql.server start
```

复制
![](https://ask.qcloudimg.com/http-save/yehe-3615093/5c43d3f8dcc69923190955bf0d38b108.png?imageView2/2/w/1620)

**当然mysql服务也可以配置开机自启动：**
**Linux 6&7 通用配置方式：**
```javascript
cp /soft/mysql/support-files/mysql.server /etc/init.d/mysqld
```

复制
![](https://ask.qcloudimg.com/http-save/yehe-3615093/3e943b0a049c1a8c74cf6a9a4593067f.png?imageView2/2/w/1620)

**配置完之后就可以用 `server mysqld start` 启动mysql服务。**
**Linux7配置方式：**
```javascript
##配置mysqld.service文件：
cat <<EOF>>/usr/lib/systemd/system/mysqld.service
[Unit]
Description=MySQL Server
Documentation=man:mysqld(8)
Documentation=http://dev.mysql.com/doc/refman/en/using-systemd.html
After=network.target
After=syslog.target
[Install]
WantedBy=multi-user.target
[Service]
User=mysql
Group=mysql
ExecStart=/soft/mysql/bin/mysqld --defaults-file=/etc/my.cnf
LimitNOFILE = 5000
EOF
```

复制
![](https://ask.qcloudimg.com/http-save/yehe-3615093/53fe032437dd16582e467d45da78a9c3.png?imageView2/2/w/1620)

**配置完之后就可以用 `systemctl start mysqld` 启动mysql服务。**
![](https://ask.qcloudimg.com/http-save/yehe-3615093/cb09e76d123c405ba6c5b4a0f114dbff.png?imageView2/2/w/1620)

**尝试连接mysql数据库：`mysql -uroot -pyhfvt_rP,24M`**
![](https://ask.qcloudimg.com/http-save/yehe-3615093/835027c148d41c32a08e9af768bca161.png?imageView2/2/w/1620)

**由于初始密码不好记，因此需要修改root初始密码：**

mysqladmin命令可参考：[mysqladmin 命令详解](https://www.cnblogs.com/dadonggg/p/8625500.html)

-   **重设root密码：`mysqladmin -uroot -pyhfvt_rP,24M password mysql`**
![](https://ask.qcloudimg.com/http-save/yehe-3615093/35917cb0996454fbfb04dfc8d7985fb1.png?imageView2/2/w/1620)

-   **用新密码连接mysql数据库：`mysql -uroot -pmysql`**
![](https://ask.qcloudimg.com/http-save/yehe-3615093/72a9d2161c3223c1309427f7fd731789.png?imageView2/2/w/1620)

-   **查看当前已创建的数据库：**
![](https://ask.qcloudimg.com/http-save/yehe-3615093/bcf430bc9cc11e3d9752c3528de6f37d.png?imageView2/2/w/1620)

-   查看数据库mysql的用户信息：
![](https://ask.qcloudimg.com/http-save/yehe-3615093/458032d1d0b1faa85328e5eee2c613ea.png?imageView2/2/w/1620)

![](https://ask.qcloudimg.com/http-save/yehe-3615093/224dde482e0705b1797c1b053d2667be.png?imageView2/2/w/1620)