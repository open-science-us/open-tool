# [Apache Hadoop](https://hadoop.apache.org)

## Installation and Configuration on Mac

~~~
[Setup passphraseless ssh]

ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa

cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys

ssh localhost

[Installation] 

wget http://apache.arvixe.com/hadoop/common/hadoop-2.6.3/hadoop-2.6.3.tar.gz

tar zxvf hadoop-2.6.3.tar.gz

cd hadoop-2.6.3

[Configuration]

vi etc/hadoop/core-site.xml

<configuration>
    <property>
    	<name>hadoop.tmp.dir</name>
  	<value>/work/hadoop/hadoop-2.7.1/tmp</value>
    </property>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>


vi etc/hadoop/hdfs-site.xml

<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>

bin/hdfs namenode -format

sbin/start-dfs.sh

http://localhost:50070/

vi etc/hadoop/mapred-site.xml

<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>


vi etc/hadoop/yarn-site.xml

<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>


sbin/start-yarn.sh

http://localhost:8088/
~~~


