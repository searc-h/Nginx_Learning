## commit命令

- docker commit提交容器副本使之成为一个心的镜像

    - docker commit -m="介绍" -a="作者" ID Name:[Tag]

- 举例：创建一个具有Vim功能的ubuntu，并commit为一个镜像(注意加速器)
    - sudo apt-get vim 
    - docker ps 查看ubuntu容器ID
    - docker commit  -m='images with vim-ubuntu' ID -a="DengH" ubuntu-vim:1.0
    - 返回一个镜像ID
    - docker images 查看刚刚创建的镜像

## 发布到阿里云镜像
- 具体看视频



## 创建私有仓库（不适用dockerHub，也不使用aliyun）
- docker pull registry
- docker run -d -p 5000:5000 -v 容器卷 --previleged=true  registry
- 将带有ifconfig的ubtunt提交到本地镜像
- 配置docker对http的支持
- push
- 检测
- pull使用
