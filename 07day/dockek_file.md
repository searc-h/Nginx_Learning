## Dockerfile基础学习

### 关键字
- FROM #基础镜像，一切从这里开始构建
- MAINTAINER #镜像是谁写的，名字+邮箱
- RUN #镜像构建的时候被需要运行的命令
- ADD #步骤，tomcat镜像，这个tomcat压缩包，添加内容
- WORKDIR #镜像的挂载目录，启动服务后的路径
- VOLUME #挂载的目录
- EXPOST #保留端口配置
- CMD #指定这个容器启动的时候要运行的命令，只有之后一个会生效，可被替代
- ENTRYPOINT #指定这个容器启动的时候要运行的命令，可以追加命令
- COPY #类似ADD，将我们文件拷贝到镜像中
- ENV #构建的时候设置环境变量
- 例如：
    ```
    [root@node143 dockerfile]# vim mydockerfile

    FROM centos
    MAINTAINER xiaoshimei<12345645@qq.com>

    ENV MYPATH /usr/locat
    WORKDIR $MYPATH

    RUN yum -y install vim
    RUN yum -y install net-tools

    EXPOSE 80

    CMD echo $MYPATH
    CMD echo"----end----"
    CMD /bin/bash  

    ```

- docker image ls -f dangling=true #查看虚悬镜像
- docker image prune #删除所有的虚悬镜像


### 练习ubuntu + vim + ifconfig
- 创建Dockerfile
    ```
        vim Dockerfime
    ```
- 编写Dockerfile
    ```
        FROM ubuntu
        MAINTAINER dh<dh@qq.com>

        ENV MYPATH /user/local
        WORKDIR $MYPATH
        RUN apt-get updatte
        RUN apt-get install net-tools
        RUN apt-get install vim

        EXPOSE 80
        
        CMD echo $MYPATH
        CMD echo "install success"
        CMD echo /bin/bash
    ```
- 构建
    ```
        docker build -t myubt:1.0
    ```
- 运行
    ```
        docker images 查看构建的镜像文件
        docker run 即可
    ```

- 同样我们可以创建微服务，打包，编写Dockerfile ，构建镜像，运行测试
