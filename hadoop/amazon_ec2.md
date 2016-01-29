# Installation and Configuraion on Amazon EC2
~~~
[Installation]

sudo yum install cmake
sudo yum install openssl-devel
sudo yum install zlib zlib-devel

# zlib-1.2.3-29.el6.i686.rpm
# zlib-1.2.3-29.el6.x86_64.rpm
# zlib-devel-1.2.3-29.el6.x86_64.rpm

curl -OL http://www.interior-dsgn.com/apache/hadoop/common/hadoop-2.6.0/hadoop-2.6.0.tar.gz

tar xzvf hadoop-2.6.0.tar.gz


[Configuration]

sudo mkdir /var/lib/hadoop
sudo chown ec2-user:ec2-user /var/lib/hadoop

sudo mkdir /var/lib/hadoop/apache
sudo chown ec2-user:ec2-user /var/lib/hadoop/apache


sudo mkdir /mnt/hadoop
sudo chown ec2-user:ec2-user /mnt/hadoop

sudo mkdir /mnt2/hadoop
sudo chown ec2-user:ec2-user /mnt2/hadoop

sudo mkdir /mnt/hadoop/apache
sudo chown ec2-user:ec2-user /mnt/hadoop/apache

sudo mkdir /mnt2/hadoop/apache
sudo chown ec2-user:ec2-user /mnt2/hadoop/apache


vi etc/hadoop/hadoop-env.sh

export JAVA_HOME=/usr/lib/jvm/jdk1.7.0_71

# export HADOOP_PREFIX=/home/ec2-user/hadoop/hadoop-2.6.0

# export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
# export HADOOP_OPTS="$HADOOP_OPTS -Djava.library.path=$HADOOP_HOME/lib/native"

export HADOOP_LOG_DIR=/var/lib/hadoop/apache

export HADOOP_PID_DIR=/var/lib/hadoop/apache


vi etc/hadoop/core-site.xml

<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://172.31.15.237:8020</value>
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
        <value>/mnt/hadoop/apache/nn,/mnt2/hadoop/apache/nn</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>/mnt/hadoop/apache/data,/mnt2/hadoop/apache/data</value>
    </property>
    <property>
        <name>dfs.client.read.shortcircuit</name>
        <value>true</value>
    </property>
    <property>
        <name>dfs.domain.socket.path</name>
        <value>/var/lib/hadoop/apache/dn_socket</value>
    </property>
</configuration>


vi etc/hadoop/yarn-site.xml

<configuration>
    <property>
        <name>yarn.resourcemanager.hostname</name>
        <value>172.31.15.238</value>
    </property>
    <property>
        <name>yarn.nodemanager.local-dirs</name>
        <value>/mnt/hadoop/apache/yarn,/mnt2/hadoop/apache/yarn</value>
    </property>
    <property>
        <name>yarn.nodemanager.log-dirs</name>
        <value>/var/lib/hadoop/apache/yarn</value>
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
        <value>172.31.15.238:10020</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.webapp.address</name>
        <value>172.31.15.238:19888</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.intermediate-done-dir</name>
        <value>/var/lib/hadoop/apache/mapred</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.done-dir</name>
        <value>/var/lib/hadoop/apache/mapred</value>
    </property>
</configuration>


vi slaves

172.31.15.237
172.31.15.238
172.31.15.239


bin/hdfs namenode -format

sbin/start-dfs.sh

http://52.25.68.242:50070/


sbin/start-yarn.sh

http://52.27.252.192:8088/

ps auwx | grep java
~~~


