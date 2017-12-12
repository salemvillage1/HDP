MYSQL			: mysql -u root -p
LOGIN AS HDFS	: su -hdfs
CHMOD			: hdfs dfs -chown -R root:hdfs /user/root
sqoop list-databases \
  --connect "jdbc:mysql://sandbox.hortonworks.com:3306" \
  --username root \
  --password hadoop

sqoop list-tables \
  --connect "jdbc:mysql://sandbox.hortonworks.com:3306/ranger" \
  --username root \
  --password hadoop

sqoop eval \
  --connect "jdbc:mysql://sandbox.hortonworks.com:3306/ranger" \
  --username root \
  --password hadoop \
  --query "select count(1) from x_service"

#NOT WORKING for Second Time:
sqoop import \
  --connect "jdbc:mysql://sandbox.hortonworks.com:3306/ranger" \
  --driver com.mysql.jdbc.Driver \
  --username root \
  --password hadoop \
  --table x_service \
  --as-textfile \
  --target-dir /home/hdfs/inbound/xservice2

 
sqoop import-all-tables \
  --connect "jdbc:mysql://sandbox.hortonworks.com:3306/ranger" \
  --driver com.mysql.jdbc.Driver \
  --username root \
  --password hadoop \
  --warehouse-dir /home/hdfs/inbound 

hadoop fs -ls /home/hdfs/inbound 
