## 容器卷
- 使用容器数据卷的方式完成数据的持久化重要数据备份
- 容器内数据 -> 持久化到本地主机目录中
- 容器卷数据独立于容器的生命周期，不会因为Docker的删除而被删除
- 实时、同步备份（与cp，import的区别）

### 如何使用--命令
- docker run -it --privileged=true -v /宿主机绝对路径:/容器内目录 镜像名

- docker run -it -v /home/dhubt/desktop/host_docker_data:/tmp/docker_data（默认rw，可指定为rw或者ro） --privileged=true ubuntu
    - 容器只读 or
- 进入容器中的/tmp/docker_data 创建文件 touch test.txt
- 进入主机的/home/dhubt/desktop/host_docker_data查看文件

- docker inspect 容器ID  查看里面的Mounts路径

- docker rm 容器ID
- docker run -it -v /home/dhubt/desktop/host_docker_data:/tmp/docker_data（默认rw，可指定为rw或者ro） --privileged=true ubuntu

- 查看文件还在，并且是最新的

