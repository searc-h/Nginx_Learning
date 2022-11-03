## Linux容器与Linux虚拟机的区别
### 虚拟机：
- 宿主计算机 -> Vmware -> 镜像内核文件 -> 特定操作系统的计算机 -> 运行某些服务（应用）

- 运行整个操作系统

- 虚拟机则适合部署LAMP这种应用椎的场景（Linux，Apache ，Mysql ， Php）


### 容器
- 容器技术 -> 打包镜像文件 -> 运行在容器中 -> 提供特定功能的应用

- 主要用于特定的应用软件

- 使用容器的一个关键性好处就是如果一个应用程序在容器中可以运行，那么任何支持这个容器的操作系统系统上都可以在不需要太多配置的情况下直接运行这个应用软件。通过容器，可以在不同的操作系统上快速部署应用，可以说容器提供了应用软件便携性。

- 容器对于跨平台快速部署应用有意义


### Ubuntu安装Docker
- [Ubuntu安装](https://blog.csdn.net/u012563853/article/details/125295985)
- [Ubuntu安装](https://huaweicloud.csdn.net/633122ded3efff3090b5367c.html)


### 申请阿里云镜像地址

### docker基础命令
- docker images 查看所有镜像
- docker search redis 本地以及hub中搜索redis镜像
- docker pull redis:6.0 / redis:latest  拉取镜像
- docker rmi redis/Id 删除镜像
- docker ps 查看所有正在运行的容器实例
    - docker ps -a
    - docker ps -l 
    - docker ps -n 
    - docker ps -m

- docker run [optioins] IMAGES [command] [arg...]  基于镜像生成容器实例
    - options: 
        - --name ：为容器分配自定义名字
        - -it ：启动交互式容器（前台伪终端，等待交互）
        - -P（大写） : 系统分配随机端口
        - -p（小写）: 指定端口映射

    - 例如：
        - docker run -it ubuntu /bin/bash
        希望交互式终端配置该容器，并使用shell终端


