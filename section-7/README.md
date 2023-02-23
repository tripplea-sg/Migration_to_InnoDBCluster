# Enterprise Encryption with InnoDB Cluster
Install plugin
```
# login to 3306
mysql -uroot -h::1 --skip-binary-as-hex

CREATE FUNCTION asymmetric_decrypt RETURNS STRING SONAME 'openssl_udf.so';
CREATE FUNCTION asymmetric_derive RETURNS STRING SONAME 'openssl_udf.so';
CREATE FUNCTION asymmetric_encrypt RETURNS STRING SONAME 'openssl_udf.so';
CREATE FUNCTION asymmetric_sign RETURNS STRING SONAME 'openssl_udf.so';
CREATE FUNCTION asymmetric_verify RETURNS INTEGER SONAME 'openssl_udf.so';
CREATE FUNCTION create_asymmetric_priv_key RETURNS STRING SONAME 'openssl_udf.so';
CREATE FUNCTION create_asymmetric_pub_key RETURNS STRING SONAME 'openssl_udf.so';
CREATE FUNCTION create_dh_parameters RETURNS STRING SONAME 'openssl_udf.so';
CREATE FUNCTION create_digest RETURNS STRING SONAME 'openssl_udf.so';

exit;
```
Set generate invisible primary key
```
mysql -uroot -h::1 -e "set persist sql_generate_invisible_primary_key=1;"
mysql -uroot -h::1 -P3307 -e "set persist sql_generate_invisible_primary_key=1;"
mysql -uroot -h::1 -P3308 -e "set persist sql_generate_invisible_primary_key=1;"
```
Login to 3306 as apps and encrypt table
```
mysql -uapps -papps -h::1 --skip-binary-as-hex
create table world_x.city_info_encrypted as select id, name, countrycode, district, hex(aes_encrypt(info, hex(keyring_key_fetch('MyKey')))) info from world_x.city;
exit;
```
Query table on 3306
```
mysql -uapps -papps -h::1 --skip-binary-as-hex -e "select id, name, countrycode, district, aes_decrypt(unhex(info), hex(keyring_key_fetch('MyKey'))) from world_x.city_info_encrypted;"
```
Query table on 3307
```
mysql -uapps -papps -h::1 --skip-binary-as-hex -e "select id, name, countrycode, district, aes_decrypt(unhex(info), hex(keyring_key_fetch('MyKey'))) from world_x.city_info_encrypted;"
```
Query table on 3308
```
mysql -uapps -papps -h::1 --skip-binary-as-hex -e "select id, name, countrycode, district, aes_decrypt(unhex(info), hex(keyring_key_fetch('MyKey'))) from world_x.city_info_encrypted;"
```
