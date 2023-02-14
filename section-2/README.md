# InnoDB Cluster
## Create instance 3307
### Create Directories
Run the following to create directory for 3307
```
mkdir -p /home/opc/db/3307/data /home/opc/db/3307/innodb_data_home_dir /home/opc/db/3307/innodb_undo_directory /home/opc/db/3307/innodb_temp_tablespace_dir /home/opc/db/3307/innodb_temp_data_file_path /home/opc/db/3307/innodb_log_group_home_dir /home/opc/db/3307/log_bin
```
### Create Option File
Create option file on /home/opc/db/3307
```
vi /home/opc/db/3307/my.cnf
```
Copy below content into vi
```
[mysqld]
datadir=/home/opc/db/3307/data
binlog-format=ROW
log-bin=/home/opc/db/3307/log_bin/bin
innodb_data_home_dir=/home/opc/db/3307/innodb_data_home_dir
innodb_undo_directory=/home/opc/db/3307/innodb_undo_directory
innodb_temp_tablespaces_dir=/home/opc/db/3307/innodb_temp_tablespace_dir 
innodb_temp_data_file_path=/home/opc/db/3307/innodb_temp_data_file_path/ibtmp1:12M:autoextend
innodb_log_group_home_dir=/home/opc/db/3307/innodb_log_group_home_dir
port=3307
server_id=20
socket=/home/opc/db/3307/data/mysqld.sock
log-error=/home/opc/db/3307/data/mysqld.log
enforce_gtid_consistency = ON
gtid_mode = ON
log_slave_updates = ON
innodb_buffer_pool_size=1G
innodb_buffer_pool_instances=1
innodb_log_file_size=1G
innodb_log_files_in_group=3
innodb_flush_log_at_trx_commit=1
```
### Create Database
Use initialize-insecure to create database with no root password
```
mysqld --defaults-file=/home/opc/db/3307/my.cnf --initialize-insecure
```
### Start Database
```
mysqld_safe --defaults-file=/home/opc/db/3307/my.cnf &
```
## Create instance 3308
### Create Directories
Run the following to create directory for 3308
```
mkdir -p /home/opc/db/3308/data /home/opc/db/3308/innodb_data_home_dir /home/opc/db/3308/innodb_undo_directory /home/opc/db/3308/innodb_temp_tablespace_dir /home/opc/db/3308/innodb_temp_data_file_path /home/opc/db/3308/innodb_log_group_home_dir /home/opc/db/3308/log_bin
```
### Create Option File
Create option file on /home/opc/db/3308
```
vi /home/opc/db/3308/my.cnf
```
Copy below content into vi
```
[mysqld]
datadir=/home/opc/db/3308/data
binlog-format=ROW
log-bin=/home/opc/db/3308/log_bin/bin
innodb_data_home_dir=/home/opc/db/3308/innodb_data_home_dir
innodb_undo_directory=/home/opc/db/3308/innodb_undo_directory
innodb_temp_tablespaces_dir=/home/opc/db/3308/innodb_temp_tablespace_dir 
innodb_temp_data_file_path=/home/opc/db/3308/innodb_temp_data_file_path/ibtmp1:12M:autoextend
innodb_log_group_home_dir=/home/opc/db/3308/innodb_log_group_home_dir
port=3308
server_id=30
socket=/home/opc/db/3308/data/mysqld.sock
log-error=/home/opc/db/3308/data/mysqld.log
enforce_gtid_consistency = ON
gtid_mode = ON
log_slave_updates = ON
innodb_buffer_pool_size=1G
innodb_buffer_pool_instances=1
innodb_log_file_size=1G
innodb_log_files_in_group=3
innodb_flush_log_at_trx_commit=1
```
### Create Database
Use initialize-insecure to create database with no root password
```
mysqld --defaults-file=/home/opc/db/3308/my.cnf --initialize-insecure
```
### Start Database
```
mysqld_safe --defaults-file=/home/opc/db/3308/my.cnf &
```
