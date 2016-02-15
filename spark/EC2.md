### Configuration on Amazon EC2

~~~
vi conf/spark-env.sh

SPARK_MASTER_IP=172.30.2.99
SPARK_DAEMON_MEMORY=256m


vi conf/slaves

172.30.2.99
172.30.2.100
172.30.2.101


sbin/start-master.sh
sbin/start-slaves.sh
sbin/start-all.sh

sbin/stop-slaves.sh 
sbin/stop-master.sh
sbin/stop-all.sh


sbin/start-slaves.sh spark://172.30.2.215:7077


ps auwx | grep spark

netstat -at | grep 7077


http://52.0.97.143:8080		(master)
http://52.0.97.143:8081		(worker)
http://52.0.97.143:4040		(driver)
http://52.71.57.224:8081	(worker)
http://52.7.96.232:8081 	(worker)


bin/spark-shell --master spark://172.30.2.99:7077 \
--conf spark.executor.memory=4096m --conf spark.driver.memory=1024m \
--conf spark.serializer=org.apache.spark.serializer.KryoSerializer
~~~
