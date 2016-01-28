# [Apache Flume](https://flume.apache.org)

## Installation and Configuration on Mac

~~~
cd /work/flume

wget http://apache.arvixe.com/flume/1.6.0/apache-flume-1.6.0-bin.tar.gz

tar -xzvf apache-flume-1.6.0-bin.tar.gz

cd apache-flume-1.6.0-bin


[Test - netcat]

cp conf/flume-conf.properties.template conf/flume-conf.properties.netcat

vi conf/flume-conf.properties.netcat

agent.sources = netcat
agent.channels = memoryChannel
agent.sinks = loggerSink

agent.sources.netcat.type = netcat
agent.sources.netcat.bind = localhost
agent.sources.netcat.port = 5555
agent.sources.netcat.channels = memoryChannel

agent.channels.memoryChannel.type = memory
agent.channels.memoryChannel.capacity = 100

agent.sinks.loggerSink.type = logger
agent.sinks.loggerSink.channel = memoryChannel


bin/flume-ng agent --conf conf --conf-file conf/flume-conf.properties.netcat --name agent -Dflume.root.logger=INFO,console


<use another terminal>

telnet localhost 5555

Hello world! <ENTER>
~~~
