## Mysql服务

### 安装mysql:5.7
- docker pull mysql:5.7
- docker run --name mysqlTest -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7 (配置密码，容器名称，后台运行，默认3306端口)
- docker exec -it ID /bin/bash (记得进入容器才能使用mysql)
- mysql -u root -p 
- show databases;
- create schema test;
- use test;
- create table t1(id int , name varcahr(20));
- insert into t1 values(01,'liming');
- select * from t1;



### 解决数据备份
- 命令如下
    ```
        docker run -d -p 3306:3306 --privileged=true
        -v /home/dhubt/Desktop/mysql/log:/var/log/mysql
        -v /home/dhubt/Desktop/mysql/data:/var/lib/mysql
        -v /home/dhubt/Desktop/mysql/conf:/etc/mysql/conf.c
        -e MYSQL_ROOT_PASSWORD=123456 
        --name mysqlTest 
        mysql:5.7
    ```
### 解决中文字符的问题
- SHOW VARIABLES LIKE 'character%' 查看字符集


