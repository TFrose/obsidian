---
author: TFrose
createtime: 2022-11-15 15:13
aliases: 未命名
description:
tags: [note]
---

## 环境准备
1、安装依赖
```text
yum install -y yum-utils device-mapper-persistent-data lvm2
```
2、添加软件源
```text
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo  # 指定阿里云镜像源
```
3、安装docker-ce（对系统内核有一定要求，centos6不支持）
```text
yum clean all  yum makecache fast        # 重新生成缓存
yum -y install docker-ce docker-ce-cli containerd.io
```
4、设置自启并启动
```text
systemctl enable docker
systemctl start docker
```
5、查看版本
```text
docker version
```
## 示例
1、搜索并下载镜像
```text
docker search nginx
docker pull nginx
```
2、启动一个容器并映射端口到本地
```text
docker run -d -p 8080:80 --name Nginx nginx    # 参数详解见下文
```
![[Pasted image 20221115151854.png]]
3、访问本地映射端口
![[Pasted image 20221115151911.png]]
## docker常用命令
1.镜像控制
```text
搜索镜像：docker  search  [OPTIONS]  TERM
上传镜像：docker  push  [OPTIONS]  NAME[:TAG]
下载镜像：docker  pull  [OPTIONS]  NAME[:TAG]
提交镜像：docker  commit [OPTIONS]  CONTAINER  NAME[:TAG]
构建镜像：docker  build  [OPTIONS]  PATH
删除镜像：docker  rmi [OPTIONS]  IMAGE  [IMAGE...]
增加镜像标签：docker  tag  SOURCE_IMAGE[:TAG]  TARGET_IMAGE[:TAG]
查看所有镜像：docker  images  [OPTIONS]  [REPOSITORY[:TAG]]
```
2.容器控制
```text
启动/重启容器：docker start/restart CONTAINER
停止/强停容器：docker stop/ kill CONTAINER
删除容器：docker rm [OPTIONS] CONTAINER [CONTAINER...]
重命名容器：docker rename CONTAINER CONTAINER_NEW
进入容器：docker attach CONTAINER
执行容器命令：docker exec CONTAINER COMMAND
查看容器日志：docker logs [OPTIONS] CONTAINER
查看容器列表：docker ps [OPTIONS]
```
![[Pasted image 20221115152108.png]]
3.容器启动
```text
docker  run  [OPTIONS]  IMAGE  [COMMAND]  [ARG...]
-d : 后台运行容器，并返回容器ID
-i：以交互模式运行容器，通常与 -t 同时使用
-t：为容器重新分配一个伪输入终端，通常与 -i 同时使用
-v：绑定挂载目录
--name="mycontainer": 为容器指定一个名称
--net="bridge": 指定容器的网络连接类型，支持如下：
     bridge / host / none / container:<name|id>
-p/-P :端口映射，格式如图：
```
![[Pasted image 20221115152148.png]]
4.其他命令
```text
查看docker信息：docker info
docker命令帮助：docker run --help
复制文件到容器：docker cp custom.conf Nginx:/etc/nginx/conf.d/
更新容器启动项：docker container update --restart=always nginx
查看docker日志：tail -f /var/log/messages
```
![[Pasted image 20221115152443.png]]