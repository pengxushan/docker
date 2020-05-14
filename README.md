# docker
docker入门

#什么是docker?
类似VM虚拟机一样的虚拟技术，但更准确的说法，其实应该是一个虚拟环境，但是docker比VM虚拟机更加轻量级、更快，更加易于移植。

#docker的生命周期
镜像：Image，可以被用户相互分享文件，例如window重装系统，首先需要一个iso镜像文件，然后才能进行系统的重装,类比一下，Docker中也有这个东西，镜像是静态的，你不能对他操作，只能pull别人的镜像或者push自己的镜像.

容器：Container，可以理解为容器是镜像动态状态，比如说window通过iso镜像安装之后的状态，前面有提到镜像只能被分享和下载不能被操作，但是容器是能被操作的.

仓库：Repository，类似于git和gitHub仓库,docker仓库是用来包含镜像的位置，当用户创建了自己的镜像之后就可以使用push命令将它上传到公有或者私友的仓库，这样在另外一台客户端如果需要使用直接pull下来就可以了.


#doker安装
https://www.widuu.com/chinese_docker/installation/windows.html

#docker的使用（Linux）



