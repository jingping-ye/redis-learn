# Redis高级应用

- Redis命令大小写不敏感

## 适合全体类型的常用命令

- 启动redis服务和redis-cli命令界面

```bash
sudo service redis-server start
sudo su
cd
redis-cli
```

- exists: 判断key是否存在，存在返回1，否则返回0

```bash
exists mykey
```

- del : 删除键和一系列键，删除成功返回1，失败返回0（key值不存在）
  - 删除一个不存在的键，返回0
  - 批量删除存在的键和不存在的键，返回1

```bash
del key
del key1 key2
```

- type:返回key元素对应值得数据类型
  -  none: 不存在
  - string:字符
  - list:列表
  - set:元组
  - zset:有序集合
  - hash:哈希

```bash
type key
```

- keys:返回匹配的key列表

```bash
# 返回所有键
keys *

# 返回以my开头的键
keys my*
```

- randomkey:随机获取一个存在的key,列表为空，返回空字符串

```bash
randomkey
```

- clear：清除界面
- rename:更改key的名字

```bash
rename key newkey
```

- renamenx:更新key的名字，key如果存在，则更新失败

```bash
set a 1 b 2
renamenx a b
```

- dbsize:返回当前数据库的key的总数

```bash
dbsize
```



## Redis时间相关命令

- expire: 设置失效时间，单位为秒

```bash
# 10秒后过期删除
expire key 10

# 10秒后返回nil
get key
```

- ex: 设置键值对的同时设置失效时间

```bash
# 设置键值对 f=>50,失效时间10秒
set f 50 ex 10
```

- ttl: 查询key还有多长时间过期
  - key不存在返回-2

```bash
ttl key
```

- flushsb:清空当前数据库所有的键
- flushall:清空所有数据库中的所有键

## Redis设置相关命令

- 可以通过`redis.conf`修改配置
- config:设置和修改命令

```bash
# 设置密码
config get requirepass  # 查看密码
config set requirepass test123  # 设置密码为 test123
config get requirepass  # 报错，没有认证
auth test123  # 认证密码
config get requirepass

# 查询数据类型的最大条目
config get *max-*-entries*

# 重置报告
config resetstat
```

## 查询信息

- info:
  - server: Redis server 的常规信息
  - clients: Client 的连接选项
  - memory: 存储占用相关信息
  - persistence: RDB and AOF 相关信息
  - stats: 常规统计
  - replication: Master/Slave 请求信息
  - cpu: CPU 占用信息统计
  - cluster: Redis 集群信息
  - keyspace: 数据库信息统计
  - all: 返回所有信息
  - default: 返回常规设置信息