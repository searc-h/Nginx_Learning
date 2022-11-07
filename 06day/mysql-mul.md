## mysql主从搭建
1. 新建主服务器容器实例3307(主机端口3307：服务器mysql端口3306)
    - docker run -p 3307:3306 --name mysql-master
2. 进入/mydata/mysql-master/conf目录新建my.cnf

3. 修改配置重启master实例

4. 进入mysql-master容器

5. master容器实例中创建数据同步用户

6. 新建从服务器容器实例3308

7. 进入/mydata/mysql-slave/conf目录新建my.cnf

8. 修改配置容器slave实例

9. 在主数据库中查看主从同步状态

10. 进入mysql-slave 容器

11. 在从数据库中配置主从复制

12. 在从数据库中查看主从同步状态

13. 在从数据库中开启主从同步

14. 查看从数据库状态发现已经同步

15. 主从复制测试