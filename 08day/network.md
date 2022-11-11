### Docker 网络
- bridge
- host
- none
- container
- 自定义网络


1. docker run -p 8081:8080 -d --name tomcat81 tomcat-jdk8
    - 默认采用bridge模式，通过docker0网路进行桥接
    - 相当于局域网中的ip地址，每个brideg网络模式的容器都是一个linux内容，拥有自己的虚拟网卡，容器与容器之间是一个局域网，容器与主机之间也是同一个局域网，通过主机的docker0网络进行桥接


2. docker run -p 8082:8080 -d --network host --name tomcat82 tomcat-jdk8
    - 相当于docker run -d --nextwork host --name tomcat82 tomcat-djk8
    - 这个时候就没必要端口映射了，因为该容器使用的是主机的ip地址，占用主机的8080端口

3. docker run --network none -d --name tomcat83 tomcat-jdk8
    - 在none模式下，并不为Docker容器进行任何的网络配置，没有Ip，没有网卡以及路由，只有localhost,需要我们自己配置ip
    - 了解即可

4. docker run -it --name alpine1 alpine /bin/sh
    - docker run -it  --network alpine1  --name alpine2 alpine /bin/sh
        - 先创建alpine1容器，使用brideg模式
        - 在创建alpine2容器，使用alpine1的网络ip，如果alpine1关闭，那么alpine2也将失去网络
        - alpine是linux的发行版

5. 自定义网络解决ping容器名（服务名）可以正常ping通
    - docker network create dh_network
    - docker run -d -p 8081:8080 --network dh_network -d --name tomcat81 tomcat-jdk8
    - docker run -d -p 8082:8080 --network dh_network -d --name tomcat82 tomcat-jdk8
    - docker exec -it tomcat82 bash
        - ping tomcat81
    

