# 1mysql登录命令

mysql -u root -p  123456

退出命令

​	exit/quit

清屏命令

​	cls

# 2mysql基本操作

show databases;

use [databasename];

show tables;

select *from [tablename];

drop tables

# 3一些实用的操作

迁移数据

insert into [table]
  select *
    from [table]
commit;