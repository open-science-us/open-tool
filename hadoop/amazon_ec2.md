# Installation and Configuraion on Amazon EC2

## Installation
~~~
sudo yum install cmake
sudo yum install openssl-devel
sudo yum install zlib zlib-devel

mkdir /home/ec2-user/hadoop
cd /home/ec2-user/hadoop

curl -OL http://apache.arvixe.com/hadoop/common/hadoop-2.6.3/hadoop-2.6.3.tar.gz

tar xzvf hadoop-2.6.3.tar.gz
~~~

## Configuration
~~~
sudo mkdir /var/lib/hadoop
sudo chown ec2-user:ec2-user /var/lib/hadoop

sudo mkdir /var/lib/hadoop/apache-2.6.3
sudo chown ec2-user:ec2-user /var/lib/hadoop/apache-2.6.3


sudo mkdir /mnt/hadoop
sudo chown ec2-user:ec2-user /mnt/hadoop

sudo mkdir /mnt/hadoop/apache-2.6.3
sudo chown ec2-user:ec2-user /mnt/hadoop/apache-2.6.3


cd /home/ec2-user/hadoop/hadoop-2.6.3

vi etc/hadoop/hadoop-env.sh

export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_66

export HADOOP_LOG_DIR=/var/lib/hadoop/apache-2.6.3

export HADOOP_PID_DIR=/var/lib/hadoop/apache-2.6.3


vi etc/hadoop/core-site.xml

<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://172.30.2.101:8020</value>
    </property>
    <property>
        <name>io.file.buffer.size</name>
        <value>131072</value>
    </property>
</configuration>


vi etc/hadoop/hdfs-site.xml

<configuration>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>/mnt/hadoop/apache-2.6.3/nn</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>/mnt/hadoop/apache-2.6.3/data</value>
    </property>
    <property>
        <name>dfs.client.read.shortcircuit</name>
        <value>true</value>
    </property>
    <property>
        <name>dfs.domain.socket.path</name>
        <value>/var/lib/hadoop/apache-2.6.3/dn_socket</value>
    </property>
</configuration>


vi etc/hadoop/yarn-site.xml

<configuration>
    <property>
        <name>yarn.resourcemanager.hostname</name>
        <value>172.30.2.101</value>
    </property>
    <property>
        <name>yarn.nodemanager.local-dirs</name>
        <value>/mnt/hadoop/apache-2.6.3/yarn</value>
    </property>
    <property>
        <name>yarn.nodemanager.log-dirs</name>
        <value>/var/lib/hadoop/apache-2.6.3/yarn</value>
    </property>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>


vi etc/hadoop/mapred-site.xml

<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.address</name>
        <value> 172.30.2.101:10020</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.webapp.address</name>
        <value> 172.30.2.101:19888</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.intermediate-done-dir</name>
        <value>/var/lib/hadoop/apache-2.6.3/mapred</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.done-dir</name>
        <value>/var/lib/hadoop/apache-2.6.3/mapred</value>
    </property>
</configuration>


vi slaves

172.30.2.99
172.30.2.100
172.30.2.101


bin/hdfs namenode -format

sbin/start-dfs.sh

http://52.7.96.232:50070/


sbin/start-yarn.sh

http://52.7.96.232:8088/

ps auwx | grep java
~~~


