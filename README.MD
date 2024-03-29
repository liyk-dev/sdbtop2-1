# SequoiaDB 集群管理工具

根据数据库管理员日常运维场景进行设计，使用菜单选择的交互方式，简化运维命令，信息使用二维表格的方式呈现，方便快速的进行筛选、排序和比对。本工具可以帮助您：

+ 快速了解集群架构、状态、服务器资源

+ 数据库、表的定义，及数据分布、节点参数

+ 管理数据库会话，包括SQL层和存储层，提供 kill 会话的功能

+ 管理数据库事务，查看事务锁等待，访问计划的执行情况

+ 监控数据库的数据读写，表的热点分区

+ 查看数据库、表的空间占用情况

## 使用环境

经过验证，能够稳定运行在以下操作系统

+ Centos 6、Centos 7、Redhat 6、Redhat 7、SUSE 11、SUSE 12

经过验证，能够稳定运行在以下数据库版本

+ 2.8.*、3.2.*、3.4.*、5.0.*

## 工具安装

```shell
tar -zxvf sdbtop2.tar.gz
cd sdbtop2
```

修改当前目录下的.conf配置文件，执行./sdbtop2 即可使用

## 配置项

需要修改以下连接配置

如果sdb版本是2.8.*，需修改配置

```txt
cluster_version = 2
```

SDB连接配置

```txt
[sdb]
cluster_name = Test
# 协调节点地址，可配置多个，以逗号分隔
cluster_coord = 127.0.0.1:11810
cluster_user = sdbadmin
cluster_passwd = 
```

MySQL 连接配置(如果没安装mysql，可删除此处配置)

```txt
[mysql]
# MySQL地址，可配置多个，以逗号分隔
mysql_hosts = sdb
mysql_port = 3306
mysql_user = root
mysql_passwd = 
```

PostgreSQL 连接配置(如果没安装postgresql，可删除此处配置)

```txt
[postgresql]
# PostgreSQL地址，可配置多个，以逗号分隔
pg_hosts = sdb
pg_port = 5432
pg_user = sdbadmin
pg_passwd = 
```

## 常用问题

+ 无法启动 sdbtop2

如果出现以下错误，或页面字符错位，则需要按q退出，在终端执行：
export TERM="xterm"
![image](https://user-images.githubusercontent.com/16267209/133355547-f9359b40-968f-428d-a5d9-c4167a129364.png)

+ 无法选中菜单项

可以调整终端设置中的Terminal为xterm，并选中ANSI Color。

## 功能详情

+ 主界面：

![image](https://user-images.githubusercontent.com/16267209/133196816-40c9e27e-23d6-4bba-a543-0633a85a3294.png)

菜单入口说明：

| 菜单  |  说明 |
|  ----  | ----  |
| 查看集群拓扑结构  | 集群的部署结构，健康状态及软件安装和数据存储位置 |
| 查看集群资源  | 集群的服务器资源情况（CPU、内存、磁盘） |
| 查看资源元数据  | 域、库、表、索引的定义，节点的参数配置 |
| 查看数据库会话  | 数据库会话管理，实时查看数据库运行的SQL和任务 |
| 查看事务和锁  | 数据库的事务和锁，执行计划 |
| 读写性能分析  | 分析数据库的读写压力分布 |
| 查看集群容量  | 数据库、表的磁盘空间占用情况 |

通用功能：

动画简单演示了按键的使用（右下角对键盘动作进行了回显）

![通用功能](https://user-images.githubusercontent.com/16267209/133299197-96dd8bf9-98db-4cfb-b6b8-148bea07147b.gif)


下面简单介绍下按键的功能，提供以下的通用按键:

| 按键  | 功能 | 说明 |
|  ----  | ----  | ----  |
| 上下方向键 | 切换菜单项 | 切换要进入的菜单功能项 |
| 回车  | 展示详情 | 进入子菜单或查看资源详情 |
| 左右箭头 < 和 >  | 移动屏幕 | 对内容超过屏幕宽度的页面，移动屏幕展示 |
| 左右方向键  | 数据分页 | 对数据较多的页面，进行分页显示 |
| 字符/  | 名称搜索 | 按名称，进行模糊搜索 |
| 字符?  | 模糊搜索 | 按行文本内容，进行模糊搜索（对查询结果进行过滤，可能会不全） |
| 字符q  | 返回上级菜单 | 返回上一层和退出程序 |

+ 查看集群拓扑结构：

![拓扑](https://user-images.githubusercontent.com/16267209/133204488-d5e96d2e-cd6b-43aa-bb37-91e7d1b1c06c.gif)

| 按键  | 功能 | 说明 |
|  ----  | ----  | ----  |
| 字符c | 切换显示模式 | 显示所有节点或只显示异常节点 |

+ 查看集群物理资源：

![资源](https://user-images.githubusercontent.com/16267209/133300492-70d65f20-d528-4046-90e3-7224c297066b.gif)


| 按键  | 功能 | 说明 |
|  ----  | ----  | ----  |
| 字符c | 切换显示模式 | 显示所有节点或只显示异常节点 |
| 回车 | 查看详情 | 显示选择主机上的节点列表 |

+ 查看资源元数据：

| 菜单  |  说明 |
|  ----  | ----  |
| 数据域列表  | 展示集群数据域 |
| 集合空间列表  | 展示集群集合空间 |
| 集合列表  | 展示集合信息 |
| 序列列表  | 展示表的自增序列信息 |
| SequoiaDB配置列表  | 展示SequoiaDB节点的配置信息 |
| MySQL配置列表  | 展示MySQL节点的配置信息 |

以集合列表为例：

![集合列表](https://user-images.githubusercontent.com/16267209/133207321-c137c87a-0aa9-4e41-a05a-8efbda45d201.gif)

| 按键  | 功能 | 说明 |
|  ----  | ----  | ----  |
| 字符m | 显示主表 | 仅显示集群的主表 |
| 字符s | 显示子表 | 默认子表是隐藏的，展示子表列表 |
| 回车 | 查看详情 | 显示选择表上的索引、表分区信息 |

+ 查看数据库会话：

| 菜单  |  说明 |
|  ----  | ----  |
| MySQL 会话列表  | 展示MySQL实例组会话 |
| PostgreSQL 会话列表  | 展示PostgreSQL实例组会话 |
| SequoiaDB 会话列表  | 展示SequoiaDB会话 |
| SequoiaDB 上下文列表  | 展示SequoiaDB上下文信息 |

以MySQL会话列表为例：

![会话](https://user-images.githubusercontent.com/16267209/133303241-c1cd7fa5-25fe-4eb4-a0f9-ee86e44fac83.gif)

| 按键  | 功能 | 说明 |
|  ----  | ----  | ----  |
| 字符r | 刷新列表 | 刷新会话列表 |
| 回车 | 查看详情 | 显示关联的SequoiaDB会话信息 |
| 字符k | 终结会话 | 强制终结执行中的SQL |

+ 查看事务和锁：

![事务](https://user-images.githubusercontent.com/16267209/133305580-bb3d51df-9fe3-49ac-9854-566665dc1e19.gif)

| 菜单  |  说明 |
|  ----  | ----  |
| 事务锁列表  | 展示事务列表，及其持有的锁信息|
| 慢查询列表  | 展示数据库的慢会话|
| 访问计划列表  | 展示表的访问计划信息|

+ 读写性能分析：

![读写分许](https://user-images.githubusercontent.com/16267209/133304686-44bacc33-0abd-462f-bcb8-3e105345c69b.gif)

| 菜单  |  说明 |
|  ----  | ----  |
| 实时监控集群读写  | 监控集群、主机、节点的读写压力情况  |
| 实时监控数据库读写  | 监控某个库下各表读写压力情况  |
| 实时监控数据表读写  | 监控某张表在各个分区上的读写情况|
| 历史性能分析  | 分析一段时间内，数据库的读写情况 |

+ 查看集群容量

![容量](https://user-images.githubusercontent.com/16267209/133304165-50f5da57-c567-4de6-b0a0-1d06a03dd281.gif)

| 按键  | 功能 | 说明 |
|  ----  | ----  | ----  |
| 字符c | 切换排序方式 | 按记录数/容量排序 |
