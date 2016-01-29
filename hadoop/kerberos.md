# Authentication with Kerberos

~~~
klist -e -k -t nn.service.keytab


ktadd -norandkey -k nn.service.keytab nn/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM


xst -norandkey -k hdfs.keytab hdfs/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM HTTP/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM


xst -norandkey -k nn.service.keytab nn/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM

xst -k nn.service.keytab nn/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM


delprinc $hdfs/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
delprinc $mapred/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
delprinc $yarn/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM

~~~
