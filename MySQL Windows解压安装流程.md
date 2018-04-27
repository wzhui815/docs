# Mysql 解压版安装步骤：

1. 下载安装包，解压安装包

2. 使用管理员权限启动cmd

3. 执行安装：bin\mysqld --install

4. 初始化数据库配置，将配置文件命名为my.ini，放到bin目录：

[mysqld]
basedir=D:\mysql-5.7.18-winx64
datadir=D:\mysql-5.7.18-winx64\data

5. 执行数据库初始化：bin\mysqld --initialize --user=mysql --console

``` log
E:\mysql-5.7.22-win32>bin\mysqld --initialize --user=mysql --console
2018-04-27T14:26:55.064275Z 0 [Warning] TIMESTAMP with implicit DEFAULT value is deprecated. Please use --explicit_defaults_for_timestamp server option (see documentation for more details).
2018-04-27T14:26:55.662189Z 0 [Warning] InnoDB: New log files created, LSN=45790
2018-04-27T14:26:55.830163Z 0 [Warning] InnoDB: Creating foreign key constraint system tables.
2018-04-27T14:26:55.948729Z 0 [Warning] No existing UUID has been found, so we assume that this is the first time that this server has been started. Generating a new UUID: 09911277-4a27-11e8-a33f-74867a1bbec5.
2018-04-27T14:26:55.977810Z 0 [Warning] Gtid table is not ready to be used. Table 'mysql.gtid_executed' cannot be opened.
2018-04-27T14:26:56.014531Z 1 [Note] A temporary password is generated for root@localhost: 4yQpDgj0Es)!
```
6. 启动数据库服务：net start mysql

7. 连接数据库修改密码，密码为临时密码：bin\mysql -u root -p

8. 修改密码：set password = password('root')
   修改后的密码为root

# 注意事项
1. 如果需要再次初始化数据库，记着删除data文件，然后运行命令即可
