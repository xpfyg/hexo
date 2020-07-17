---
title: InfluxDB
date: 2020-07-17 17:05:51
tags:
---
文档

https://jasper-zhang1.gitbooks.io/influxdb/content/Guide/writing_data.html

https://www.cnblogs.com/gaoguangjun/p/8513032.html

https://blog.csdn.net/yue530tomtom/article/details/82625561

https://segmentfault.com/a/1190000018862405#articleHeader6

**sharding**

https://blog.csdn.net/suzy1030/article/details/81459029

启动

- Mac

brew services start influxdb

- 

连接

- 连接本地

influx -precision rfc3339

- 连接远程

influx -host 39.106.178.240 -port 8086 -password shopex123 -username shopex -precision rfc3339

创建 InfluxDB

文档

https://jasper-zhang1.gitbooks.io/influxdb/content/Guide/writing_data.html

https://www.cnblogs.com/gaoguangjun/p/8513032.html

https://blog.csdn.net/yue530tomtom/article/details/82625561

https://segmentfault.com/a/1190000018862405#articleHeader6

**sharding**

https://blog.csdn.net/suzy1030/article/details/81459029

启动

- Mac

brew services start influxdb

- 

连接

- 连接本地

influx -precision rfc3339

- 连接远程

influx -host 39.106.178.240 -port 8086 -password shopex123 -username shopex -precision rfc3339

创建

> create database cadvisor ## 创建数据库cadvisor

> show databases

name: databases

name

----

_internal

cadvisor

> CREATE USER testuser WITH PASSWORD 'testpwd' ## 创建用户和设置密码

> GRANT ALL PRIVILEGES ON cadvisor TO testuser ## 授权数据库给指定用户

> create user “username” with password ‘password’ with all privileges ## 创建管理元用户

> CREATE RETENTION POLICY "cadvisor_retention" ON "cadvisor" DURATION 30d REPLICATION 1 DEFAULT ## 创建默认的数据保留策略，设置保存时间30天，副本为1
InfluxDB

文档

https://jasper-zhang1.gitbooks.io/influxdb/content/Guide/writing_data.html

https://www.cnblogs.com/gaoguangjun/p/8513032.html

https://blog.csdn.net/yue530tomtom/article/details/82625561

https://segmentfault.com/a/1190000018862405#articleHeader6

**sharding**

https://blog.csdn.net/suzy1030/article/details/81459029

启动

- Mac

brew services start influxdb

- 

连接

- 连接本地

influx -precision rfc3339

- 连接远程

influx -host 39.106.178.240 -port 8086 -password shopex123 -username shopex -precision rfc3339

创建

> create database cadvisor ## 创建数据库cadvisor

> show databases

name: databases

name

----

_internal

cadvisor

> CREATE USER testuser WITH PASSWORD 'testpwd' ## 创建用户和设置密码

> GRANT ALL PRIVILEGES ON cadvisor TO testuser ## 授权数据库给指定用户

> create user “username” with password ‘password’ with all privileges ## 创建管理元用户

> CREATE RETENTION POLICY "cadvisor_retention" ON "cadvisor" DURATION 30d REPLICATION 1 DEFAULT ## 创建默认的数据保留策略，设置保存时间30天，副本为1

> create database cadvisor ## 创建数据库cadvisor

> show databases

name: databases

name

----

_internal

cadvisor

> CREATE USER testuser WITH PASSWORD 'testpwd' ## 创建用户和设置密码

> GRANT ALL PRIVILEGES ON cadvisor TO testuser ## 授权数据库给指定用户

> create user “username” with password ‘password’ with all privileges ## 创建管理元用户

> CREATE RETENTION POLICY "cadvisor_retention" ON "cadvisor" DURATION 30d REPLICATION 1 DEFAULT ## 创建默认的数据保留策略，设置保存时间30天，副本为1

查询条件

查询教程 [https://www.cnblogs.com/yihuihui/p/11386691.html](https://www.cnblogs.com/yihuihui/p/11386691.html)

value 如果是字符则用单引号

select * from "order_pool" where "tid"='1072849218408210376'

select count(amount) from order_pool where time>1593360000s and time<1593964800s

select top(count,1) from (select count(amount) from order_pool group by to_node_type limit 1)
