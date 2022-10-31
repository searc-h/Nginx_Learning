## 使用Nginx配置虚拟主机与多站点

### 修改C:\Windows\System32\drivers\etc 下的hosts
1. 在hosts中添加ip与对应的域名
![hosts]('https://github.com/searc-h/Nginx_Learning/tree/master/02day/images/hosts.png')
2. 注意这里的ip填写虚拟机的ip地址（也可以是公网ip地址）

3. 切记修改之后把hosts的权限设置应用到默认（小新DNS劫持） 

### 修改Nginx配置
> 默认conf文件路径 /etc/nginx/sites-enabled/default
> 默认html文件路径 /var/www/html/.html

    1. 一个server对应一个主机

    2. 每个server的 （端口，域名）值不能相同

    3. 一个ip可以有多个域名（serverName）

    4. 一个域名可以有多个二级域名(com 顶级域名，qq一级域名，dh二级域名)

    > 例如: dh.qq.com , cyd.qq.com

### HttpDNS
- [HttpDNS介绍](https://blog.csdn.net/a745233700/article/details/102559761) 

- [httpDNS是什么技术](https://baijiahao.baidu.com/s?id=1738462861602951475&wfr=spider&for=pc)

- [两者的区别](https://blog.csdn.net/sanmi8276/article/details/110387143)

- >总结：基于TCP的DNS域名解析服务，解决传统DNS解析服务的一些安全与效率问题，不过这个也带来了另一些局限。


### 负载均衡
- weight  权重
- down  挂掉
- backup 备用


### 动静分离
- 让Nginx来直接返回静态文件，减小了后端服务器压力

> 伪静态：rewrite


