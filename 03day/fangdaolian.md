## 防盗链

### http referrer的作用

### nginx配置防盗链

### curl测试防盗链
- 安装curl
```bash
    #直接访问站点资源，不带referrer
    curl -I 'http://192.168.177.128/img/logo.png'

    #在referrer='http://baidu.com'下，访问站点资源
    curl -e "http://baidu/com" -I "ttp://192.168.177.128/img/logo.png"

```


## keepAlive 实现多nginx的高可用

## https 以及 AC认证