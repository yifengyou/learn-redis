# Redis安装

## CentOS 7 环境下

yum简单安装

``` bash
# 安装 Redis
yum install redis -y
```

基本配置

``` bash
# 配置 Redis
echo 'vm.overcommit_memory = 1' >> /etc/sysctl.conf
sysctl -p
sed -i '@^daemonize no@daemonize yes@g' /etc/redis.conf
sed -i 's@^bind 127.0.0.1@bind 0.0.0.0@g' /etc/redis.conf
sed -i 's@^appendonly no@appendonly yes@g' /etc/redis.conf
# ${REDIS_PSWD} 自己定义成数据库管理员密码
echo "requirepass ${REDIS_PSWD}" >> /etc/redis.conf
```

设定开机启动

``` bash
# 启动并使其随机启动
systemctl enable redis.service
systemctl start redis.service
```

简单功能测试

```bash

# ${REDIS_PSWD} 自己定义成数据库管理员密码  ${HOST}为Redis服务端ip，未设定则为本机localhost ,默认端口 6379
# 基本格式如下
# redis-cli -h ${HOST} -p port -a ${REDIS_PSWD}
# ping回复PONG则说明连通


[root@iZbp136jwir14u4w7i4o74Z ~]# redis-cli -h localhost -p 6379 -a youyifeng
localhost:6379> ping
PONG

```

服务端口查看

```
[root@iZbp136jwir14u4w7i4o74Z ~]# netstat -anpt | grep redis
tcp        0      0 0.0.0.0:6379            0.0.0.0:*               LISTEN      19088/redis-server  
tcp        0      0 172.16.9.184:6379       117.175.129.42:38891    ESTABLISHED 19088/redis-server
```







---
