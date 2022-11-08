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
        docker run -d -p 3306:3306 --privileged=true \
        -v /home/dhubt/Desktop/mysql/log:/var/log/mysql \
        -v /home/dhubt/Desktop/mysql/data:/var/lib/mysql \
        -v /home/dhubt/Desktop/mysql/conf:/etc/mysql/conf.d \
        -e MYSQL_ROOT_PASSWORD=123456 \
        --name mysqlTest \
        mysql:5.7
    ```
### 解决中文字符的问题
- SHOW VARIABLES LIKE 'character%' 查看字符集

- 主机进入/home/dhubt/Desktop/mysql/conf中新建my.cnf
- 在my.cnf中输入 ，并保存
    ```
        [client]
        default_character_set=utf8
        [mysqld]
        collation_server = utf8_general_ci
        character_set_server = utf8
    ```
- cat  my.cnf查看是否保存成功

- 重启mysql容器实例
    - docker restart 容器ID或者Name

- 进入mysqlTest容器
    - docker exec -it ID /bin/bash (记得进入容器才能使用mysql)
    - mysql -u root -p 
    - show databases;
    - create schema test;
    - use test;
    - create table t1(id int , name varcahr(20));
    - insert into t1 values(01,'liming');
    - select * from t1;
- docker rm -f mysqlTest 强制删除该容器

- 重新启动
    ```
        docker run -d -p 3306:3306 --privileged=true
        -v /home/dhubt/Desktop/mysql/log:/var/log/mysql
        -v /home/dhubt/Desktop/mysql/data:/var/lib/mysql
        -v /home/dhubt/Desktop/mysql/conf:/etc/mysql/conf.d
        -e MYSQL_ROOT_PASSWORD=123456 
        --name mysqlTest 
        mysql:5.7
    ```

- 再次进入，查看原始数据还在不在


### 解决WorkBench连接数据库失败问题
- Hostname:192.168.177.128
- Port:3306
- Username:root
- Password:123456

### workbench字符集
- alert table修改即可




