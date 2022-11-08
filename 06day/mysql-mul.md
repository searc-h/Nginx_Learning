## mysql主从搭建
1. 新建主服务器容器实例3307(主机端口3307：服务器mysql端口3306)

        ```
            docker run -d -p 3307:3306 --privileged=true \
            -v /home/dhubt/Desktop/mysql-master/log:/var/log/mysql \
            -v /home/dhubt/Desktop/mysql-master/data:/var/lib/mysql \
            -v /home/dhubt/Desktop/mysql-master/conf:/etc/mysql\
            -e MYSQL_ROOT_PASSWORD=123456 \
            --name mysql-master \
            mysql:5.7
        ```
2. 进入/home/dhubt/Desktop/mysql-master/conf目录新建my.cnf(也可以创建文件修改，再执行第一步)
    ```bash
    [mysqld]
    ## 设置server_id，同一局域网中需要唯一
    server_id=101
    ## 指定不需要同步的数据库名称
    binlog-ignore-db=mysql
    ## 开启二进制日志gongn
    log-bin=mall-mysql-bin
    ## 设置二进制日志使用的内存大小（事务）
    binlog_cache_size=1M
    ## 设置使用二进制日志格式（mixed , statement , row）
    binlog_format=mixed
    ## 二进制日志过期清理时间，默认值为0 ，表示不自动清理
    expire_logs_days=7
    ## 跳过主从复制中遇到的所有错误或指定类型的错误，避免slave端复制中断
    ## 如：1062错误是指一些主键重复，1032错误是因为主从数据库不一致
    slave_skip_errors=1062
    ```

3. 修改配置重启master实例

4. 进入mysql-master容器

5. master容器实例中创建数据同步用户
    ```bash 
    ## 授权
    CREATE USER 'slave'@'%' IDENTIFIED BY '123456';
    GRANT REPLICATION SLAVE,REPLICATION CLIENT ON *.* TO 'slave'@'%';
    ```

6. 新建从服务器容器实例3308
    ```
    docker run -d -p 3308:3306 --privileged=true \
    -v /home/dhubt/Desktop/mysql-slave/log:/var/log/mysql \
    -v /home/dhubt/Desktop/mysql-slave/data:/var/lib/mysql \
    -v /home/dhubt/Desktop/mysql-slave/conf:/etc/mysql\
    -e MYSQL_ROOT_PASSWORD=123456 \
    --name mysql-slave \
    mysql:5.7
    ```
7. 进入/mydata/mysql-slave/conf目录新建my.cnf
    ```bash
    [mysqld]
    ## 设置server_id，同一局域网中需要唯一
    server_id=102
    ## 指定不需要同步的数据库名称
    binlog-ignore-db=mysql
    ## 开启二进制日志gongn
    log-bin=mall-mysql-slave-bin
    ## 设置二进制日志使用的内存大小（事务）
    binlog_cache_size=1M
    ## 设置使用二进制日志格式（mixed , statement , row）
    binlog_format=mixed
    ## 二进制日志过期清理时间，默认值为0 ，表示不自动清理
    expire_logs_days=7
    ## 跳过主从复制中遇到的所有错误或指定类型的错误，避免slave端复制中断
    ## 如：1062错误是指一些主键重复，1032错误是因为主从数据库不一致
    slave_skip_errors=1062
    ## relay_log配置中继日志
    relay_log=mall-mysql-relay-bin
    ## log_slave_updates表示slave将复制事件写进自己的二进制日志
    log_slave_updates=1
    ## slave设置为只读
    read_only=1
    ```
8. 修改配置后重启容器slave实例

9. 在主数据库mysql-master中查看主从同步状态
- 进入mysql服务
- show master status 

10. 进入mysql-slave容器

11. 在从数据库中配置主从复制
- 认老大 master
    ```
    chang master to master_host='192.168.177.128',master_user='slave', master_password='123456', master_port=3307 , master_log_file='mall-mysql-bin.000001',master_log_pos=617,master_connect_retry=30;
    ```

12. 在从数据库中查看主从同步状态
    ```
    show slave status \G;
    ```
13. 在从数据库中开启主从同步
- 同意接受
    ```
        start slave;
    ```

14. 查看从数据库状态发现已经同步    
    ```
        show slave status \G;
    ```

15. 主从复制测试
- 主数据库添加记录
- 从数据自动备份