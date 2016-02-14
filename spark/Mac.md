### Configuration on Mac

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
