# [Kerberos](http://web.mit.edu/kerberos/)

## Installation on Amazon EC2

~~~
sudo yum install krb5-server krb5-libs krb5-auth-dialog krb5-workstation

cp /etc/krb5.conf /etc/krb5.conf.bak

sudo vi /etc/krb5.conf

[realms]
 TPS.COM = {
  kdc = ip-172-31-19-127.us-west-2.compute.internal
  admin_server = ip-172-31-19-127.us-west-2.compute.internal
 }

[domain_realm]
 tps.com = TPS.COM

/usr/sbin/kdb5_util create -s

# master key name 'K/M@TPS.COM'  password: abc123

/usr/sbin/kdb5_util create -s -r TPS.COM

# master key name 'K/M@TPS.COM'  password: abc123

sudo vi /var/kerberos/krb5kdc/kadm5.acl

# */admin@TPS.COM *

sudo /usr/sbin/kadmin.local -q "addprinc ec2-user/admin"

# password: abc123

sudo /sbin/service krb5kdc start

sudo /sbin/service kadmin start

sudo kadmin.local -q listprincs

sudo chown ec2-user:ec2-user /var/log/kadmind.log


mkdir /home/ec2-user/keytabs

cd /home/ec2-user/keytabs

kadmin

addprinc -randkey hdfs/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
addprinc -randkey mapred/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
addprinc -randkey yarn/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
addprinc -randkey HTTP/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM

addprinc -randkey nn/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
addprinc -randkey sn/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
addprinc -randkey dn/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM

addprinc -randkey rm/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
addprinc -randkey nm/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
addprinc -randkey jhs/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM

addprinc -randkey host/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM


xst -k hdfs.keytab hdfs/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM HTTP/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
xst -k mapred.keytab mapred/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM HTTP/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
xst -k yarn.keytab yarn/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM HTTP/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM


xst -k nn.service.keytab nn/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM host/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
xst -k sn.service.keytab sn/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM host/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
xst -k dn.service.keytab dn/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM host/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM

xst -k rm.service.keytab rm/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM host/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
xst -k nm.service.keytab nm/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM host/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
xst -k jhs.service.keytab jhs/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM host/ip-172-31-19-127.us-west-2.compute.internal@TPS.COM
~~~
