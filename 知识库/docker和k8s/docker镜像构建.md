---
author: TFrose
createtime: 2022-11-15 15:25
aliases: 未命名
description:
tags: [note]
---

## docker镜像
1.Docker commit（1运行2修改3保存）
```text
#运行容器
docker run -dit -p 8080:80 --name Nginx nginx
#修改容器（这里我只是做个演示，所以就复制一下文件，具体修改需要根据你实际情况）
docker cp custom.conf Nginx:/etc/nginx/conf.d/
#将容器保存为新的镜像
docker commit Nginx zwx/nginx
```
![[Pasted image 20221115153007.png]]
2.Dockerfile（1编写2构建）

```text
#编写Dockerfile文件
vim Dockerfile
#执行Dockerfile文件
docker build -t zwx/nginx . #后面有个点，代表当前目录下dockerfile文件
```
![[Pasted image 20221115153210.png]]
3.Dockerfile 常用指令
![[Pasted image 20221115153553.png]]
## docker本地仓库
1、拉取镜像仓库

```text
docker search registry
docker pull registry
```
2、启动镜像服务

```text
docker run -dit 
--name=Registry   # 指定容器名称
-p 5000:5000     # 仓库默认端口是5000，映射到宿主机，这样可以使用宿主机地址访问
--restart=always    # 自动重启，这样每次docker重启后仓库容器也会自动启动
--privileged=true   # 增加安全权限，一般可不加
-v /usr/local/my_registry:/var/lib/registry      # 把仓库镜像数据保存到宿主机
registry
```
3、注册https协议（需要通过本地仓库下载镜像，均需要配置）

```text
vim /etc/docker/daemon.json # 默认无此文件，需自行添加，有则追加一下内容。
   { "insecure-registries":[" xx.xx.xx.xx:5000"] 
   }  #指定ip地址或域名
```
4、新增tag指明仓库地址

```text
docker tag zwx/nginx x.xx.xx.xx:5000/zwx/nginx  # 如果构建时已经指定仓库地址，则可以省略
```
5、上传镜像到本地仓库

```text
docker push x.xx.xx.xx:5000/zwx/nginx
```
6、查看本地仓库

```text
curl -XGET http://x.xx.xx.xx:5000/v2/_catalog
```
![[Pasted image 20221115154124.png]]
