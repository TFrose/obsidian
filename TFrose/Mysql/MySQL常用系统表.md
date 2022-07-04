## MySQL5.7 默认模式
| 库名                 | 表数量 | 视图数量 |
|--------------------|-----|------|
| information_schema | 61  | 0    |
| mysql              | 32  | 0    |
| performance_schema | 87  | 0    |
| sys                | 1   | 100  |

## Information_schema
Information_schema数据库是MySQL自带的，它提供了访问数据库元数据的方式。

**什么是元数据呢？**
元数据是关于数据的数据，如数据库名或表名，列的数据类型，或访问权限等。有些时候用于表述该信息的其他术语包括“数据词典”和“系统目录”。
在MySQL中，把 information_schema 看作是一个数据库，确切说是信息数据库。其中保存着关于MySQL服务器所维护的所有其他数据库的信息。如数据库名，数据库的表，表栏的数据类型与访问权限等。在INFORMATION_SCHEMA中，有数个只读表。它们实际上是视图，而不是基本表，因此，你将无法看到与之相关的任何文件。

**information_schema 数据库部分表说明**
| 表名                                    | 注释                                                                                                                    |
|---------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| SCHEMATA                              | 提供了当前mysql实例中所有数据库的信息。show databases的结果取之此表                                                                          |
| TABLES                                | 提供了关于数据库中的表的信息（包括视图）。详细表述了某个表属于哪个schema、表类型、表引擎、创建时间等信息。是show tables from schemaname的结果取之此表                           |
| COLUMNS                               | 提供了表中的列信息。详细表述了某张表的所有列以及每个列的信息。是show columns from schemaname.tablename的结果取之此表                                         |
| STATISTICS                            | 提供了关于表索引的信息。是show index from schemaname.tablename的结果取之此表                                                              |
| USER_PRIVILEGES                       | 用户权限表:给出了关于全程权限的信息。该信息源自mysql.user授权表。是非标准表                                                                           |
| SCHEMA_PRIVILEGES                     | 方案权限表:给出了关于方案（数据库）权限的信息。该信息来自mysql.db授权表。是非标准表                                                                        |
| TABLE_PRIVILEGES                      | 表权限表:给出了关于表权限的信息。该信息源自mysql.tables_priv授权表。是非标准表                                                                      |
| COLUMN_PRIVILEGES                     | 列权限表:给出了关于列权限的信息。该信息源自mysql.columns_priv授权表。是非标准表                                                                     |
| CHARACTER_SETS                        | 字符集表:提供了mysql实例可用字符集的信息。是SHOW CHARACTER SET结果集取之此表                                                                    |
| COLLATIONS                            | 提供了关于各字符集的对照信息                                                                                                        |
| COLLATION_CHARACTER_SET_APPLICABILITY | 指明了可用于校对的字符集。这些列等效于SHOW COLLATION的前两个显示字段。                                                                            |
| TABLE_CONSTRAINTS                     | 描述了存在约束的表。以及表的约束类型                                                                                                    |
| KEY_COLUMN_USAGE                      | 描述了具有约束的键列                                                                                                            |
| ROUTINES                              | 提供了关于存储子程序（存储程序和函数）的信息。此时，ROUTINES表不包含自定义函数（UDF）。名为“mysql.proc name”的列指明了对应于INFORMATION_SCHEMA.ROUTINES表的mysql.proc表列 |
| VIEWS                                 | 给出了关于数据库中的视图的信息。需要有show views权限，否则无法查看视图信息                                                                            |
| TRIGGERS                              | 提供了关于触发程序的信息。必须有super权限才能查看该表                                                                                         |

## performance_schema
PERFORMANCE_SCHEMA这个功能默认是关闭的。需要设置参数： performance_schema 才可以启动该功能，这个参数是静态参数，只能写在my.cnf 中 不能动态修改。
| 表名                                | 注释                                                                                                             |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------|
| setup_table                       | 设置表，配置监控选项                                                                                                     |
| current_events_table              | 记录当前那些thread 正在发生什么事情                                                                                          |
| history_table                     | 发生的各种事件的历史记录表                                                                                                  |
| summary_table                     | 对各种事件的统计表                                                                                                      |
| setup_consumers\setup_instruments | 描述各种事件, 设置哪些事件能够被收集                                                                                            |
| setup_instruments                 | 描述这个数据库下的表名以及是否开启监控                                                                                            |
| setup_timers                      | 描述监控选项已经采样频率的时间间隔                                                                                              |
| threads                           | 监控服务器所有连接                                                                                                      |
| performance_timers                | 设置一些监控信息, 指定mysql服务可用的监控周期，CYCLE表示按每秒检测2603393034次, 目前 performance-schema 只支持’wait’时间的监控，代码树上 wait/ 下的函数都可以监控到 |

## mysql
在mysql数据库中，有mysql_install_db脚本初始化权限表，存储权限的表
**mysql数据库部分表说明**
| 表名         | 注释                               |
| ------------ | ---------------------------------- |
| user         | 用户列、权限列、安全列、资源控制列 |
| db           | 用户列、权限列                     |
| host         |                                    |
| table_priv   |                                    |
| columns_priv |                                    |
| proc_priv  |                                    |

