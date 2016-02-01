# [Kerberos](http://web.mit.edu/kerberos/)

## Installation and Configuration on Amazon EC2

### Reference

(1) [how to install and configure kerberos server](http://www.slashroot.in/how-install-and-configure-kerberos-server)

### Installing Kerberos
~~~
sudo yum install krb5-server krb5-libs krb5-auth-dialog krb5-workstation
~~~

### Setting REALM for Kerberos
~~~
sudo cp /etc/krb5.conf /etc/krb5.conf.bak

sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = OPEN_TOOL.ORG

[realms]
 OPEN_TOOL.ORG = {
  kdc = ip-172-30-2-101.ec2.internal
  admin_server = ip-172-30-2-101.ec2.internal
 }

[domain_realm]
 open_tool.org = ip-172-30-2-101.ec2.internal@ OPEN_TOOL.ORG
~~~

### Creating Kerberos database
~~~
sudo /usr/sbin/kdb5_util create -s -r OPEN_TOOL.ORG

Loading random data
Initializing database '/var/kerberos/krb5kdc/principal' for realm 'OPEN_TOOL.ORG',
master key name 'K/M@OPEN_TOOL.ORG'
You will be prompted for the database Master Password.
It is important that you NOT FORGET this password.
Enter KDC database master key: 
Re-enter KDC database master key to verify: 
~~~

### Editing acl file for principals ending with /admin to get full permission
~~~
sudo vi /var/kerberos/krb5kdc/kadm5.acl

*/admin@OPEN_TOOL.ORG *
~~~

### Creating principal ec2-user/admin
~~~
sudo /usr/sbin/kadmin.local -q "addprinc ec2-user/admin"

Authenticating as principal root/admin@OPEN_TOOL.ORG with password.
WARNING: no policy specified for ec2-user/admin@OPEN_TOOL.ORG; defaulting to no policy
Enter password for principal "ec2-user/admin@OPEN_TOOL.ORG": 
Re-enter password for principal "ec2-user/admin@OPEN_TOOL.ORG": 
Principal "ec2-user/admin@OPEN_TOOL.ORG" created.
~~~

### Running Kerberos server
~~~
sudo /sbin/service krb5kdc start

sudo /sbin/service kadmin start

sudo chown ec2-user:ec2-user /var/log/kadmind.log
~~~

### Listing Kerberos principals
~~~
sudo kadmin.local -q listprincs

Authenticating as principal root/admin@OPEN_TOOL.ORG with password.
K/M@OPEN_TOOL.ORG
ec2-user/admin@OPEN_TOOL.ORG
kadmin/admin@OPEN_TOOL.ORG
kadmin/changepw@OPEN_TOOL.ORG
kadmin/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
kiprop/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
krbtgt/OPEN_TOOL.ORG@OPEN_TOOL.ORG
~~~

### Testing ec2-user/admin
~~~
mkdir /home/ec2-user/kerberos

cd /home/ec2-user/kerberos

kinit ec2-user/admin

Password for ec2-user/admin@OPEN_TOOL.ORG: 

kadmin

Authenticating as principal ec2-user/admin@OPEN_TOOL.ORG with password.
Password for ec2-user/admin@OPEN_TOOL.ORG: 

kadmin:  listprincs

K/M@OPEN_TOOL.ORG
ec2-user/admin@OPEN_TOOL.ORG
kadmin/admin@OPEN_TOOL.ORG
kadmin/changepw@OPEN_TOOL.ORG
kadmin/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
kiprop/ip-172-30-2-101.ec2.internal@OPEN_TOOL.ORG
krbtgt/OPEN_TOOL.ORG@OPEN_TOOL.ORG
~~~
