# Docker基础

## 什么是Docker?
类似VM虚拟机一样的虚拟技术，但更准确的说法，其实应该是一个虚拟环境，但是docker比VM虚拟机更加轻量级、更快，更加易于移植。

## Docker的生命周期
镜像：Image，可以被用户相互分享文件，例如window重装系统，首先需要一个iso镜像文件，然后才能进行系统的重装,类比一下，Docker中也有这个东西，镜像是静态的，你不能对他操作，只能pull别人的镜像或者push自己的镜像.

容器：Container，可以理解为容器是镜像动态状态，比如说window通过iso镜像安装之后的状态，前面有提到镜像只能被分享和下载不能被操作，但是容器是能被操作的.

仓库：Repository，类似于git和gitHub仓库,docker仓库是用来包含镜像的位置，当用户创建了自己的镜像之后就可以使用push命令将它上传到公有或者私友的仓库，这样在另外一台客户端如果需要使用直接pull下来就可以了.


## Doker安装（所有版本）
https://www.widuu.com/chinese_docker/installation/windows.html

## Docker基本运用
* 设置docker开机自启动<br>
```
systemctl enable docker
```
  
* docker的启动、重启、停止<br>
```
service docker start
service docker restart
service docker stop
```

* 查询镜像<br>
```
docker search <镜像名称>
```

* 获取镜像<br>
```
docker pull <镜像名称>
```

* 查看镜像<br>
```
 docker images：列出images
 docker images -a：列出所有的images（包含历史）
``` 
 
* 删除镜像<br>
```
 docker rmi  <image ID>
```
  
* 容器的创建（举例redis）<br>
```
1.创建redis挂载目录<br>
 mkdir -p /data/docker/redis/conf  配置文件
 mkdir -p /root/docker/redis/data  数据

2.创建容器<br>
docker run -d --privileged=true -p 6379:6379 --restart always -v /data/docker/redis/conf:/etc/redis/redis.conf -v /data/docker/redis/data:/data --name redis-test redis redis-server /etc/redis/redis.conf --appendonly yes
```
<br>

```
  -d, --detach=false         指定容器运行于前台还是后台，默认为false   
  -i, --interactive=false    打开STDIN，用于控制台交互  
  -t, --tty=false            分配tty设备，该可以支持终端登录，默认为false  
  -u, --user=""              指定容器的用户  
  -a, --attach=[]            标准输入输出流和错误信息（必须是以非docker run -d启动的容器）
  -w, --workdir=""           指定容器的工作目录 
  -c, --cpu-shares=0         设置容器CPU权重，在CPU共享场景使用  
  -e, --env=[]               指定环境变量，容器中可以使用该环境变量  
  -m, --memory=""            指定容器的内存上限  
  -P, --publish-all=false    指定容器暴露的端口  
  -p, --publish=[]           指定容器暴露的端口 
  -h, --hostname=""          指定容器的主机名  
  -v, --volume=[]            给容器挂载存储卷，挂载到容器的某个目录  
  --volumes-from=[]          给容器挂载其他容器上的卷，挂载到容器的某个目录
  --cap-add=[]               添加权限，权限清单详见：http://linux.die.net/man/7/capabilities  
  --cap-drop=[]              删除权限，权限清单详见：http://linux.die.net/man/7/capabilities  
  --cidfile=""               运行容器后，在指定文件中写入容器PID值，一种典型的监控系统用法  
  --cpuset=""                设置容器可以使用哪些CPU，此参数可以用来容器独占CPU  
  --device=[]                添加主机设备给容器，相当于设备直通  
  --dns=[]                   指定容器的dns服务器  
  --dns-search=[]            指定容器的dns搜索域名，写入到容器的/etc/resolv.conf文件  
  --entrypoint=""            覆盖image的入口点  
  --env-file=[]              指定环境变量文件，文件格式为每行一个环境变量  
  --expose=[]                指定容器暴露的端口，即修改镜像的暴露端口  
  --link=[]                  指定容器间的关联，使用其他容器的IP、env等信息  
  --lxc-conf=[]              指定容器的配置文件，只有在指定--exec-driver=lxc时使用  
  --name=""                  指定容器名字，后续可以通过名字进行容器管理，links特性需要使用名字  
  --net="bridge"             容器网络设置:
                                bridge 使用docker daemon指定的网桥     
                                host     //容器使用主机的网络  
                                container:NAME_or_ID  >//使用其他容器的网路，共享IP和PORT等网络资源  
                                none 容器使用自己的网络（类似--net=bridge），但是不进行配置 
  --privileged=false         指定容器是否为特权容器，特权容器拥有所有的capabilities  
  --restart="no"             指定容器停止后的重启策略:
                                no：容器退出时不重启  
                                on-failure：容器故障退出（返回值非零）时重启 
                                always：容器退出时总是重启  
  --rm=false                 指定容器停止后自动删除容器(不支持以docker run -d启动的容器)  
  --sig-proxy=true           设置由代理接受并处理信号，但是SIGCHLD、SIGSTOP和SIGKILL不能被代理  
```  
* 查看容器<br>
```
  docker ps    查看正在运行的容器
  docker ps -a 查看所有的容器
```   
   
* 容器的启动、重启、停止、删除<br>
```
 docker start <ContainerId(或者name)>     启动容器<br>
 docker stop <ContainerId(或者name)>      停止容器<br>
 docker restart <ContainerId(或者name)>   重启容器<br>
 docker rm <ContainerId(或者name)>        删除容器<br> 
 
 ```

* 连接容器<br>
```
docker exec -it containerID /bin/bash
```

* 查看容器日志<br>
```
docker logs -f -t --tail <行数> <容器名或者containerID>
```

* docker与宿主机之间的拷贝<br>
```
文件从宿主机拷贝到容器:  docker cp 宿主机文件路径   容器名:存放路径<br>
docker cp /home/test.txt nginx:/var/nginx_home

文件从容器拷贝到宿主机   docker cp 容器名:要拷贝的文件路径  宿主机存放路径 <br> 
docker cp nginx:/var/nginx_home/test.txt /home
```
## Docker课后作业
```
1.安装docker（环境不限）
2.docker操作（启动、重启、停止）
3.镜像操作（获取、删除、查看）
4.容器操作（查看、创建、启动、重启、停止、删除、连接、日志查看）
5.docker和宿主机之间文件拷贝
```
