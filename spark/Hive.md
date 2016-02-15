## Integration with Hive

### Building Spark package with Hive
~~~
cd /work/spark-hive

curl -O http://d3kbcqa49mib13.cloudfront.net/spark-1.6.0.tgz

tar zxvf spark-1.6.0.tgz

cd spark-1.6.0

build/mvn -DskipTests -Phive -Phive-thriftserver clean package
~~~

### Configuring Spark to integrate with Hive
~~~
cd /work/spark-hive/spark-1.6.0

cp /work/hive/apache-hive-1.2.1-bin/conf/hive-site.xml conf/

vi conf/hive-site.xml

// derby
<configuration>
  <property>
   <name>hive.metastore.warehouse.dir</name>
   <value>hdfs://localhost:8020/usr/hive/warehouse</value>
   <description>location of the warehouse directory</description>
 </property>
 <property>
   <name>hive.metastore.metadb.dir</name>
   <value>/work/hive/apache-hive-1.2.1-bin/metastore_db</value>
   <description>location of the warehouse directory</description>
 </property>
</configuration>

// mysql
<configuration>
 <property>
   <name>hive.metastore.warehouse.dir</name>
   <value>hdfs://localhost:9000/usr/hive/warehouse </value>
   <description>location of the warehouse directory</description>
 </property>
 <property>
      <name>javax.jdo.option.ConnectionURL</name>
      <value>jdbc:mysql://localhost/metastore?createDatabaseIfNotExist=true</value>
      <description>metadata is stored in a MySQL server</description>
   </property>
   <property>
      <name>javax.jdo.option.ConnectionDriverName</name>
      <value>com.mysql.jdbc.Driver</value>
      <description>MySQL JDBC driver class</description>
   </property>
   <property>
      <name>javax.jdo.option.ConnectionUserName</name>
      <value>hiveuser</value>
      <description>user name for connecting to mysql server</description>
   </property>
   <property>
      <name>javax.jdo.option.ConnectionPassword</name>
      <value>hivepassword</value>
      <description>password for connecting to mysql server</description>
   </property>
</configuration>


sbin/start-master.sh
sbin/start-slaves.sh
sbin/start-all.sh

sbin/stop-slaves.sh 
sbin/stop-master.sh
sbin/stop-all.sh


ps auwx | grep spark

netstat -at | grep 7077


http://localhost:8080		(master)
http://localhost:8081		(worker 1)
http://localhost:8082		(worker 2)
http://localhost:8083		(worker 3)
http://localhost:4040		(driver)


bin/spark-shell --master spark://localhost:7077 --jars /work/hive/apache-hive-1.2.1-bin/lib/mysql-connector-java-5.1.38.jar
~~~

### Testing
~~~
val sqlContext = new org.apache.spark.sql.hive.HiveContext(sc)

sqlContext.sql("CREATE TABLE IF NOT EXISTS test (key INT, value STRING)")

sqlContext.sql("LOAD DATA LOCAL INPATH '/work/hive/apache-hive-1.2.1-bin/examples/files/kv1.txt' INTO TABLE test")

sqlContext.sql("FROM test SELECT key, value").collect().foreach(println)

sqlContext.sql("FROM pokes SELECT foo, bar").collect().foreach(println)
~~~
