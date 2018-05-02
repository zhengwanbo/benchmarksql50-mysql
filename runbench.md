
Support tpcc test for mysql and tidb.
--------------------------------------

Run command and steps.
--------------------------------------

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
