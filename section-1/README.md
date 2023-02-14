# Migrating MariaDB to MySQL Enterprise Edition
## MariaDB database Server
Following is the MariaDB database server to be migrated:
```
IP address: 10.0.0.110
MariaDB user: apps
MariaDB password: apps
```
## Prepare MySQL Server
If you have not done so, please follow these instruction </br>
Install using TAR is flexible and stright forward. However, we have to ensure all pre-requisites are installed on. new server
For new server, RPM or YUM based installation can be use to validate any missing OS dependencies.
```
cd /home/opc/software

unzip MySQL-Server-8.0.30.zip
tar -zxvf mysql-commercial-8.0.30-el7-x86_64.tar.gz

unzip MySQL-Shell-8.0.30.zip
sudo rpm -ivh mysql-shell-commercial-8.0.30-1.1.el7.x86_64.rpm

unzip MySQL-Router-8.0.30.zip
tar -zxvf mysql-router-commercial-8.0.30-el7-x86_64.tar.gz
```
Create environment file to source MySQL Enterprise. Copy the following line and create $HOME/.8030.env file </br>
command: 
```
vi $HOME/.8030.env
```
Copy and paste to vi
```
PATH=$PATH:/home/opc/software/mysql-commercial-8.0.30-el7-x86_64/bin:/home/opc/software/mysql-router-commercial-8.0.30-el7-
```
Source environment: a process that we need to include MySQL into $PATH
```
. $HOME/.8030.env
```
Create MySQL Database Directory
```
mkdir -p /home/opc/db/3306/data /home/opc/db/3306/innodb_data_home_dir /home/opc/db/3306/innodb_undo_directory /home/opc/db/3306/innodb_temp_tablespace_dir /home/opc/db/3306/innodb_temp_data_file_path /home/opc/db/3306/innodb_log_group_home_dir /home/opc/db/3306/log_bin
```
Create option file / configuration file for the database with the following content (command: vi /home/opc/db/3306/my.cnf)
```
[mysqld]
datadir=/home/opc/db/3306/data
binlog-format=ROW
log-bin=/home/opc/db/3306/log_bin/bin
innodb_data_home_dir=/home/opc/db/3306/innodb_data_home_dir
innodb_undo_directory=/home/opc/db/3306/innodb_undo_directory
innodb_temp_tablespaces_dir=/home/opc/db/3306/innodb_temp_tablespace_dir 
innodb_temp_data_file_path=/home/opc/db/3306/innodb_temp_data_file_path/ibtmp1:12M:autoextend
innodb_log_group_home_dir=/home/opc/db/3306/innodb_log_group_home_dir
port=3306
server_id=10
socket=/home/opc/db/3306/data/mysqld.sock
log-error=/home/opc/db/3306/data/mysqld.log
enforce_gtid_consistency = ON
gtid_mode = ON
log_slave_updates = ON
innodb_buffer_pool_size=12G
innodb_buffer_pool_instances=8
innodb_log_file_size=1G
innodb_log_files_in_group=3
innodb_flush_log_at_trx_commit=1
```
Create database with random root password using the following:
```
mysqld --defaults-file=/home/opc/db/3306/my.cnf --initialize-insecure
```
Start MySQL database
```
mysqld_safe --defaults-file=/home/opc/db/3306/my.cnf 
```

