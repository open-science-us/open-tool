# [Apache Spark](http://spark.apache.org)

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




