# [Hadoop in Secure Mode](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/SecureMode.html)

## Setting up users, groups and directories
~~~
sudo groupadd -r hadoop

sudo useradd -g hadoop hdfs
sudo useradd -g hadoop yarn
sudo useradd -g hadoop mapred

sudo chown -R hdfs:hadoop /mnt/hadoop/apache-2.6.3/nn
sudo chown -R hdfs:hadoop /mnt/hadoop/apache-2.6.3/data
sudo chown -R yarn:hadoop /mnt/hadoop/apache-2.6.3/yarn
sudo chown -R mapred:hadoop /mnt/hadoop/apache-2.6.3/jh
~~~
