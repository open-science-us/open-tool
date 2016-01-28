# [Apache Sqoop](http://sqoop.apache.org)

## Installation on Mac

~~~
cd /work/sqoop

wget http://apache.arvixe.com/sqoop/1.4.6/sqoop-1.4.6.bin__hadoop-2.0.4-alpha.tar.gz

tar -xzvf sqoop-1.4.6.bin__hadoop-2.0.4-alpha.tar.gz

cd sqoop-1.4.6.bin__hadoop-2.0.4-alpha

cp conf/sqoop-env-template.sh conf/sqoop-env.sh

vi conf/sqoop-env.sh

export HADOOP_HOME=/work/hadoop/hadoop-2.6.3
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
export HIVE_HOME=/work/hive/apache-hive-1.2.1-bin

bin/sqoop version

bin/sqoop help
~~~
