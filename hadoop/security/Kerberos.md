# Authentication with Kerberos

## Reference

(1) [Hadoop in Secure Mode](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/SecureMode.html)

(2) [Installation and Configuration on Amazon EC2](https://github.com/open-science-us/open-tool/tree/master/security/kerberos)

## Adding Kerberos principals
~~~
kadmin: 

addprinc -randkey hdfs/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
addprinc -randkey mapred/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
addprinc -randkey yarn/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
addprinc -randkey HTTP/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG

addprinc -randkey nn/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
addprinc -randkey sn/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
addprinc -randkey dn/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG

addprinc -randkey rm/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
addprinc -randkey nm/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
addprinc -randkey jhs/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG

addprinc -randkey host/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
~~~

## Preparing Kerberos keytab files
~~~
xst -k hdfs.keytab hdfs/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG HTTP/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
xst -k mapred.keytab mapred/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG HTTP/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
xst -k yarn.keytab yarn/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG HTTP/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG

xst -k nn.service.keytab nn/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG host/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
xst -k sn.service.keytab sn/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG host/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
xst -k dn.service.keytab dn/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG host/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG

xst -k rm.service.keytab rm/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG host/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
xst -k nm.service.keytab nm/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG host/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
xst -k jhs.service.keytab jhs/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG host/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
~~~

## Listing Kerberos principals in Kerberos keytab files
~~~
klist -e -k -t nn.service.keytab

Keytab name: FILE:nn.service.keytab
KVNO Timestamp           Principal
---- ------------------- ------------------------------------------------------
   2 02/01/2016 15:34:35 nn/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG (aes256-cts-hmac-sha1-96) 
   2 02/01/2016 15:34:35 nn/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG (aes128-cts-hmac-sha1-96) 
   2 02/01/2016 15:34:35 nn/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG (des3-cbc-sha1) 
   2 02/01/2016 15:34:35 nn/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG (arcfour-hmac) 
   2 02/01/2016 15:34:35 host/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG (aes256-cts-hmac-sha1-96) 
   2 02/01/2016 15:34:35 host/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG (aes128-cts-hmac-sha1-96) 
   2 02/01/2016 15:34:35 host/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG (des3-cbc-sha1) 
   2 02/01/2016 15:34:35 host/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG (arcfour-hmac) 
~~~

### Authentication with Kerberos keytab file
~~~
kinit -k -t hdfs.keytab hdfs/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
~~~
