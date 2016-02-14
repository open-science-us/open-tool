# [Apache Spark](http://spark.apache.org)

## Installation and Configuration on Mac

### Downloading Spark package with Hadoop
~~~
curl -O http://d3kbcqa49mib13.cloudfront.net/spark-1.6.0-bin-hadoop2.6.tgz

tar zxvf spark-1.6.0-bin-hadoop2.6.tgz

cd spark-1.6.0-bin-hadoop2.6

bin/run-example SparkPi 10
~~~

### Building Spark package without Hadoop
~~~
curl -O http://d3kbcqa49mib13.cloudfront.net/spark-1.6.0.tgz

tar zxvf spark-1.6.0.tgz

cd spark-1.6.0

build/mvn -DskipTests clean package

bin/run-example SparkPi 10
~~~

### Configuration
~~~
vi conf/spark-env.sh

SPARK_MASTER_IP=localhost
SPARK_DAEMON_MEMORY=256m

vi conf/slaves

localhost

sbin/start-all.sh

ps auwx | grep spark

http://localhost:8080

bin/spark-shell --master spark://localhost:7077
~~~





