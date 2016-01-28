# [DataStax Cassandra](http://www.datastax.com)

## Installaion on Mac
~~~
sudo mkdir /var/lib/dse
sudo mkdir /var/log/dse

sudo chown -R scheng:staff /var/lib/dse
sudo chown -R scheng:staff /var/log/dse

cd /work/dse

curl --user <user>:<password> -OL http://downloads.datastax.com/enterprise/dse.tar.gz

tar -xzvf dse.tar.gz

cd dse-4.8.2

cd resources/cassandra/conf

mv cassandra.yaml cassandra.yaml.orig

sed 's/\/var\/lib\/cassandra/\/var\/lib\/dse/g' cassandra.yaml.orig > cassandra.yaml

cp cassandra-env.sh cassandra-env.sh.orig

vi cassandra-env.sh

JVM_OPTS="$JVM_OPTS -Xloggc:/var/log/dse/jvm/gc.log"
CASSANDRA_HEAPDUMP_DIR=/var/log/dse/jvm


cd bin

cp dse.in.sh dse.in.sh.orig

vi dse.in.sh

export CASSANDRA_LOG_DIR="/var/log/dse”


# start with Spark

bin/dse cassandra -k

ps auwx | grep dse
~~~


