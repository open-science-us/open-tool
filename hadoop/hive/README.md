# [Apache Hive](https://hive.apache.org)

## Installation on Mac

~~~
cd /work/hadoop/hadoop-2.6.3

mkdir backup
mv share/hadoop/yarn/lib/jline-0.9.94.jar backup

bin/hadoop fs -mkdir /tmp
bin/hadoop fs -mkdir /user/hive/
bin/hadoop fs -mkdir /user/hive/warehouse
bin/hadoop fs -chmod g+w /tmp
bin/hadoop fs -chmod g+w /user/hive/warehouse
bin/hadoop fs -chmod o+w /user/hive/warehouse

cd /work/hive

wget http://apache.mirrors.hoobly.com/hive/hive-1.2.1/apache-hive-1.2.1-bin.tar.gz

tar -xzvf apache-hive-1.2.1-bin.tar.gz

cd apache-hive-1.2.1-bin

export HIVE_HOME=/work/hive/apache-hive-1.2.1-bin
export PATH=$HIVE_HOME/bin:$PATH
export HADOOP_HOME=/work/hadoop/hadoop-2.6.3

bin/hive
~~~

