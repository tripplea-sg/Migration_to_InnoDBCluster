# MySQL Enterprise Backup
## Create backup administrator
The mysqlbackup command connects to the MySQL server using the credentials supplied with the --user and --password options. 
The specified user needs certain privileges. 
```
CREATE USER 'mysqlbackup'@'localhost' IDENTIFIED BY 'backup';
GRANT SELECT, BACKUP_ADMIN, RELOAD, PROCESS, SUPER, REPLICATION CLIENT ON *.* TO `mysqlbackup`@`localhost`;
GRANT CREATE, INSERT, DROP, UPDATE ON mysql.backup_progress TO 'mysqlbackup'@'localhost'; 
GRANT CREATE, INSERT, DROP, UPDATE, SELECT, ALTER ON mysql.backup_history TO 'mysqlbackup'@'localhost';
```
For creating a backup to tape using SBT API
```
grant CREATE, INSERT, DROP, UPDATE on the mysql.backup_sbt_history TO 'mysqlbackup'@'localhost'; 
```
For transportable tablespace and backup non-innodb tables
```
GRANT LOCK TABLES, CREATE, DROP, FILE, INSERT, ALTER ON *.* TO 'mysqlbackup'@'localhost';
```
For using redo log archiving
```
GRANT INNODB_REDO_LOG_ARCHIVE ON *.* TO 'mysqlbackup'@'localhost';
```
For using encrypted tablespace
```
GRANT ENCRYPTION_KEY_ADMIN ON *.* TO 'mysqlbackup'@'localhost';
```
For working with InnoDB Cluster or Group Replication
```
GRANT SELECT ON performance_schema.replication_group_members TO 'mysqlbackup'@'localhost';
```
