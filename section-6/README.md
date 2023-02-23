# Enterprise Audit with InnoDB Cluster
Install audit plugin
```
mysql -uroot -h::1 -e "INSTALL PLUGIN audit_log SONAME 'audit_log.so';"
mysql -uroot -h::1 -P3307 -e "set global super_read_only=off; INSTALL PLUGIN audit_log SONAME 'audit_log.so'; set global super_read_only=on"
mysql -uroot -h::1 -P3308 -e "set global super_read_only=off; INSTALL PLUGIN audit_log SONAME 'audit_log.so'; set global super_read_only=on"

mysql -uroot -h127.0.0.1 

CREATE TABLE IF NOT EXISTS audit_log_filter(NAME VARCHAR(64) BINARY NOT NULL PRIMARY KEY, FILTER JSON NOT NULL) engine= InnoDB CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_as_ci;
CREATE TABLE IF NOT EXISTS audit_log_user(USER VARCHAR(32) BINARY NOT NULL, HOST VARCHAR(255) BINARY NOT NULL, FILTERNAME VARCHAR(64) BINARY NOT NULL, PRIMARY KEY (USER, HOST), FOREIGN KEY (FILTERNAME) REFERENCES mysql.audit_log_filter(NAME)) engine= InnoDB CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_as_ci;
CREATE FUNCTION audit_log_filter_set_filter RETURNS STRING SONAME 'audit_log.so';
CREATE FUNCTION audit_log_filter_remove_filter RETURNS STRING SONAME 'audit_log.so';
CREATE FUNCTION audit_log_filter_set_user RETURNS STRING SONAME 'audit_log.so';
CREATE FUNCTION audit_log_filter_remove_user RETURNS STRING SONAME 'audit_log.so';
CREATE FUNCTION audit_log_filter_flush RETURNS STRING SONAME 'audit_log.so';
CREATE FUNCTION audit_log_read_bookmark RETURNS STRING SONAME 'audit_log.so';
CREATE FUNCTION audit_log_read RETURNS STRING SONAME 'audit_log.so';
CREATE FUNCTION audit_log_encryption_password_set RETURNS INTEGER SONAME 'audit_log.so';
CREATE FUNCTION audit_log_encryption_password_get RETURNS STRING SONAME 'audit_log.so';

SELECT audit_log_filter_flush() AS 'Result';
exit;
```
Check audit plugin
```
mysql -uroot -h::1 -e "show plugins; show variables like '%audit_log%'; select * from mysql.audit_log_user; select * from mysql.audit_log_filter;"
mysql -uroot -h::1 -P3307 -e "show plugins; show variables like '%audit_log%'; select * from mysql.audit_log_user; select * from mysql.audit_log_filter;"
mysql -uroot -h::1 -P3308 -e "show plugins; show variables like '%audit_log%'; select * from mysql.audit_log_user; select * from mysql.audit_log_filter;"
```
Install audit log filter to audit all activities and apply to all users
```
# login to 3306
mysql -uroot -h::1

SELECT audit_log_filter_set_filter('log_all', '{ "filter": { "log": true } }');
SELECT audit_log_filter_set_user('%', 'log_all');
select * from mysql.audit_log_user;
select * from mysql.audit_log_filter;
exit;

mysql -uroot -h::1 -P3307 -e "select audit_log_filter_flush();"
mysql -uroot -h127.0.0.1 -P3308 -e "select audit_log_filter_flush();"
```
Login to 3307 and check audit log
```
mysql -uroot -h::1 -P3307
show databases;
exit

cat /home/opc/db/3307/data/audit.log
```
