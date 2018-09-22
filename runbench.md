
Support tpcc test for mysql and tidb.
--------------------------------------

Run command and steps.
--------------------------------------

# mysql

```
#create database.
mysql -uroot -P4000 -h127.0.0.1 -e "create database tpcc"

#drop tabels.
mysql -uroot -P4000 -h127.0.0.1 -e  "truncate table tpcc5.bmsql_config"
./runSQL.sh props.mysql  tableDrops

#create tables.
./runSQL.sh props.mysql  tableCreates

#create index;
./runSQL.sh props.mysql  indexCreates

#runing after load data.
./runSQL.sh props.mysql buildFinish

#truncate tabels.
./runSQL.sh props.mysql  tableTruncates

#modify the configuration of mysql or tidb. for ex: ip and port, etc.
vi prop.mysql

#load data into tabels.
 ./runLoader.sh props.mysql

#run tpcc benchmark
./runBenchmark.sh props.mysql

```


# oracle

```
#create database.
create temporary tablespace DB_TEMP tempfile '/data/app/oracle/oradata/prod/db_temp.dbf' size 32M autoextend on next 2G maxsize unlimited extent management local;

 create temporary tablespace DB_TEMP tempfile '/data/app/oracle/oradata/prod/db_temp.dbf' SIZE 32M 
 AUTOEXTEND ON NEXT 32M MAXSIZE UNLIMITED 
 EXTENT MANAGEMENT LOCAL;

 CREATE TABLESPACE DB_DATA
 LOGGING
 DATAFILE '/data/app/oracle/oradata/prod/DB_DATA.DBF' SIZE 32M
 AUTOEXTEND ON
 NEXT 32M MAXSIZE UNLIMITED
 EXTENT MANAGEMENT LOCAL;

 CREATE USER tpccbench IDENTIFIED BY password
         ACCOUNT UNLOCK
         DEFAULT TABLESPACE DB_DATA
         TEMPORARY TABLESPACE DB_TEMP;

 GRANT CONNECT,RESOURCE TO tpccbench; 
 GRANT DBA TO tpccbench; 

sqlplus tpccbench/password 

#modify the configuration of mysql or tidb. for ex: ip and port, etc.
vi prop.ora

#modify java.security if failed by IO error.
去到$JAVA_PATH/jre/lib/security/java.security这个文件，找到下面的内容： 改为
securerandom.source=file:/dev/urandom

#drop tabels.
./runSQL.sh props.ora  tableDrops

#create tables.
./runSQL.sh props.ora  tableCreates

#create index;
./runSQL.sh props.ora  indexCreates

#truncate tabels.
./runSQL.sh props.ora  tableTruncates

#load data into tabels.
 ./runLoader.sh props.ora

#run tpcc benchmark
./runBenchmark.sh props.ora

```
