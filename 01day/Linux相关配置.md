## 下载安装Nginx服务

### 下载nginx命令 
1. sudo apt-get install nginx

### 查看nginx安装路径
1. find / -name nginx

### 开启nginx服务
1. nginx

### 查看nginx占用端口
1. 切换到root su root 
2. 更换root名称与密码 sudo passwd root
3. 查看nginx占用端口 netstat -ntlp | grep nginx 

## 本机xShell连接虚拟机

### 查看虚拟机ip地址
1. 下载net-tools sudo apt-get install net-tools
2. 查看虚拟机ip地址 ifconfig 
3. ![image]('https://github/searc-h/nginx+learn/images/ifconfig.png')

### 放行22端口 
- sudo apt-get install openssh-server
- sudo apt-get install ufw
- sudo ufw enable
- sudo ufw allow 22

### 关闭防火墙（内网使用）
- sudo  ufw enable|disable
- 查看是否开启或关闭 sudo ufw status

### 连接成功
