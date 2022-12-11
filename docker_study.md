#dock 学习
##1 注册docker账号
https://hub.docker.com/
##2 docker客户端常用命令
##### 查看docker客户端所有命令
```
docker
```
##### 查看某个命令详细用法
```
docker <command> --help
```
##### 将当前用户加入docker用户组
```
sudo groupadd docker            #添加docker用户组
sudo gpasswd -a $USER docker    #将登陆用户加入到docker用户组中
newgrp docker                   #更新用户组
docker ps                       #测试
```
### 2.1 镜像
##### 拉取镜像
```
docker pull <image>
```
##### 列出镜像
```
docker images
```
其中，
REPOSITORY：表示镜像的仓库源
TAG：镜像的标签
IMAGE ID：镜像ID
CREATED：镜像创建时间
SIZE：镜像大小
使用 REPOSITORY:TAG 来定义不同的镜像，不指定镜像TAG，默认使用latest
##### 查找镜像
```
docker search <image>
```
##### 删除镜像
```
docker rmi [-f] <img or img_id>
```
### 2.2 容器
##### 指定镜像创建容器并在容器中运行指定程序
```
docker run ubuntu:15.10 /bin/echo "Hello world"

显示容器终端
docker run -i -t ubuntu:15.10 /bin/bash

在后台执行
docker run -d ubuntu:15.10 /bin/sh -c "while true; do echo hello world; sleep 1; done"

指定名字
docker run -itd --name ubuntu-test ubuntu /bin/bash

将容器内部使用的网络端口随机映射到我们使用的主机上
docker run -d -P training/webapp python app.py
```
##### 查看容器端口映射
```
docker port
或者
docker ps
```
##### 查看容器状态
```
docker ps [-a]
```
##### 查看容器日志
```
docker logs [-f] <CONTAINER_ID or CONTAINER_NAME>
[-f]        类似tail的-f
```
##### 查看容器中进程
```
docker top
```
##### 停止容器
```
docker stop <CONTAINER_ID or CONTAINER_NAME>
```
##### 启动已停止容器
```
docker start <CONTAINER_ID or CONTAINER_NAME>
```
##### 重启容器
```
docker restart
```
##### 进入容器
```
docker attach <CONTAINER_ID or CONTAINER_NAME>
注意attach进入容器退出后，容器会停止运行

docker exec -it <CONTAINER_ID or CONTAINER_NAME> /bin/bash
exec进入容器退出后，容器会保持运行，一般用这个
```
##### 导出容器
```
docker export <CONTAINER_ID or CONTAINER_NAME> > ubuntu.tar
```
##### 导入容器
```
cat ./ubuntu.tar | docker import - test/ubuntu:v1

也可以从url或某个目录导入
docker import http://example.com/exampleimage.tgz example/imagerepo
```
##### 删除容器
```
docker rm -f <CONTAINER_ID or CONTAINER_NAME>
删除容器时，容器必须是停止状态
```

### 遇到的问题
##### docker pull失败
```
$ sudo docker pull ubuntu
Using default tag: latest
Error response from daemon: error parsing HTTP 408 response body: invalid character '<' looking for beginning of value: "<html><body><h1>408 Request Time-out</h1>\nYour browser didn't send a complete request in time.\n</body></html>
```
解决方法：
```
ifconfig ens33 mtu 900
```
设置完mtu后，重新pull，pull完后记得将mtu重新设置成1500
```
sudo ifconfig ens33 mtu 1500
```
