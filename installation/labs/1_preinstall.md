```{r, engine='bash',  System Configuration Checks}
[ec2-user@ip-172-31-7-21 ~]$ sudo sysctl -w net.ipv4.icmp_echo_ignore_all=0
[ec2-user@ip-172-31-7-21 ~]$ sudo sysctl vm.swappiness=10
[ec2-user@ip-172-31-7-21 ~]$ sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1
[ec2-user@ip-172-31-7-21 ~]$ sudo vi /etc/sysctl.conf
vm.swappines = 10
[ec2-user@ip-172-31-7-21 ~]$ findmnt
TARGET                           SOURCE      FSTYPE      OPTIONS
/                                /dev/xvda2  xfs         rw,relatime,seclabel,attr2,inode64,noquota
+-/sys                           sysfs       sysfs       rw,nosuid,nodev,noexec,relatime,seclabel
¦ +-/sys/kernel/security         securityfs  securityfs  rw,nosuid,nodev,noexec,relatime
¦ +-/sys/fs/cgroup               tmpfs       tmpfs       ro,nosuid,nodev,noexec,seclabel,mode=755
¦ ¦ +-/sys/fs/cgroup/systemd     cgroup      cgroup      rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd
¦ ¦ +-/sys/fs/cgroup/blkio       cgroup      cgroup      rw,nosuid,nodev,noexec,relatime,blkio
¦ ¦ +-/sys/fs/cgroup/perf_event  cgroup      cgroup      rw,nosuid,nodev,noexec,relatime,perf_event
¦ ¦ +-/sys/fs/cgroup/cpuset      cgroup      cgroup      rw,nosuid,nodev,noexec,relatime,cpuset
¦ ¦ +-/sys/fs/cgroup/net_cls     cgroup      cgroup      rw,nosuid,nodev,noexec,relatime,net_cls
¦ ¦ +-/sys/fs/cgroup/cpu,cpuacct cgroup      cgroup      rw,nosuid,nodev,noexec,relatime,cpuacct,cpu
¦ ¦ +-/sys/fs/cgroup/memory      cgroup      cgroup      rw,nosuid,nodev,noexec,relatime,memory
¦ ¦ +-/sys/fs/cgroup/freezer     cgroup      cgroup      rw,nosuid,nodev,noexec,relatime,freezer
¦ ¦ +-/sys/fs/cgroup/hugetlb     cgroup      cgroup      rw,nosuid,nodev,noexec,relatime,hugetlb
¦ ¦ +-/sys/fs/cgroup/devices     cgroup      cgroup      rw,nosuid,nodev,noexec,relatime,devices
¦ +-/sys/fs/pstore               pstore      pstore      rw,nosuid,nodev,noexec,relatime
¦ +-/sys/fs/selinux              selinuxfs   selinuxfs   rw,relatime
¦ +-/sys/kernel/debug            debugfs     debugfs     rw,relatime
¦ +-/sys/kernel/config           configfs    configfs    rw,relatime
+-/proc                          proc        proc        rw,nosuid,nodev,noexec,relatime
¦ +-/proc/sys/fs/binfmt_misc     systemd-1   autofs      rw,relatime,fd=28,pgrp=1,timeout=300,minproto=5,maxproto=5,direct
¦   +-/proc/sys/fs/binfmt_misc   binfmt_misc binfmt_misc rw,relatime
+-/dev                           devtmpfs    devtmpfs    rw,nosuid,seclabel,size=7599332k,nr_inodes=1899833,mode=755
¦ +-/dev/shm                     tmpfs       tmpfs       rw,nosuid,nodev,seclabel
¦ +-/dev/pts                     devpts      devpts      rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000
¦ +-/dev/hugepages               hugetlbfs   hugetlbfs   rw,relatime,seclabel
¦ +-/dev/mqueue                  mqueue      mqueue      rw,relatime,seclabel
+-/run                           tmpfs       tmpfs       rw,nosuid,nodev,seclabel,mode=755
  +-/run/user/1000               tmpfs       tmpfs       rw,nosuid,nodev,relatime,seclabel,size=1497312k,mode=700,uid=1000,gid=1000

[ec2-user@ip-172-31-7-21 ~]$ cat /etc/fstab

#
# /etc/fstab
# Created by anaconda on Tue Mar  1 18:16:26 2016
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=65722bd1-fccc-453e-a96a-8f3599aa0466 /                       xfs     defaults        0 0
[ec2-user@ip-172-31-7-21 ~]$
[ec2-user@ip-172-31-7-21 ~]$ sudo -i
[root@ip-172-31-7-21 ~]# echo never > /sys/kernel/mm/transparent_hugepage/defrag
[root@ip-172-31-7-21 ~]# echo never > /sys/kernel/mm/transparent_hugepage/enabled
[root@ip-172-31-7-21 ~]# vi /etc/rc.local
[root@ip-172-31-7-21 ~]# cat /etc/rc.local
#!/bin/bash
# THIS FILE IS ADDED FOR COMPATIBILITY PURPOSES
#
# It is highly advisable to create own systemd services or udev rules
# to run scripts during boot instead of using this file.
#
# In contrast to previous versions due to parallel execution during boot
# this script will NOT be run after all other services.
#
# Please note that you must run 'chmod +x /etc/rc.d/rc.local' to ensure
# that this script will be executed during boot.

touch /var/lock/subsys/local
echo never > /sys/kernel/mm/transparent_hugepage/defrag
echo never > /sys/kernel/mm/transparent_hugepage/enabled
[root@ip-172-31-7-21 ~]# chmod +x /etc/rc.local
[root@ip-172-31-7-21 ~]# ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 172.31.7.21  netmask 255.255.240.0  broadcast 172.31.15.255
        inet6 fe80::46d:60ff:fe5a:439  prefixlen 64  scopeid 0x20<link>
        ether 06:6d:60:5a:04:39  txqueuelen 1000  (Ethernet)
        RX packets 301524  bytes 441348066 (420.9 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 85429  bytes 6978753 (6.6 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 0  (Local Loopback)
        RX packets 4  bytes 340 (340.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 4  bytes 340 (340.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

[root@ip-172-31-7-21 ~]# yum install nscd bind-utils ntp wget install mariadb-server vim -y
[root@ip-172-31-7-21 ~]# getent hosts
127.0.0.1       localhost localhost.localdomain localhost4 localhost4.localdomain4
127.0.0.1       localhost localhost.localdomain localhost6 localhost6.localdomain6
52.59.220.8     aws1
35.158.124.217  aws2
54.93.214.27    aws3
52.59.204.70    aws4
52.59.252.72    aws5
[root@ip-172-31-7-21 ~]# nslookup aws1
Server:         172.31.0.2
Address:        172.31.0.2#53

** server can't find aws1: NXDOMAIN

[root@ip-172-31-7-21 ~]# nslookup aws2
Server:         172.31.0.2
Address:        172.31.0.2#53

** server can't find aws2: NXDOMAIN

[root@ip-172-31-7-21 ~]# nslookup aws3
Server:         172.31.0.2
Address:        172.31.0.2#53

** server can't find aws3: NXDOMAIN

[root@ip-172-31-7-21 ~]# nslookup aws4
Server:         172.31.0.2
Address:        172.31.0.2#53

** server can't find aws4: NXDOMAIN

[root@ip-172-31-7-21 ~]# nslookup aws5
Server:         172.31.0.2
Address:        172.31.0.2#53

** server can't find aws5: NXDOMAIN

[root@ip-172-31-7-21 ~]#
[root@ip-172-31-7-21 ~]# systemctl enable nscd
Created symlink from /etc/systemd/system/multi-user.target.wants/nscd.service to /usr/lib/systemd/system/nscd.service.
Created symlink from /etc/systemd/system/sockets.target.wants/nscd.socket to /usr/lib/systemd/system/nscd.socket.
[root@ip-172-31-7-21 ~]# systemctl start nscd
[root@ip-172-31-7-21 ~]# systemctl status nscd
? nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2017-06-05 10:11:49 EDT; 1min 16s ago
 Main PID: 28890 (nscd)
   CGroup: /system.slice/nscd.service
           +-28890 /usr/sbin/nscd

Jun 05 10:11:49 ip-172-31-7-21.eu-central-1.compute.internal nscd[28890]: 28890 monitoring directory `/etc` (2)
Jun 05 10:11:49 ip-172-31-7-21.eu-central-1.compute.internal nscd[28890]: 28890 monitoring file `/etc/resolv.conf` (5)
Jun 05 10:11:49 ip-172-31-7-21.eu-central-1.compute.internal nscd[28890]: 28890 monitoring directory `/etc` (2)
Jun 05 10:11:49 ip-172-31-7-21.eu-central-1.compute.internal nscd[28890]: 28890 monitoring file `/etc/services` (6)
Jun 05 10:11:49 ip-172-31-7-21.eu-central-1.compute.internal nscd[28890]: 28890 monitoring directory `/etc` (2)
Jun 05 10:11:49 ip-172-31-7-21.eu-central-1.compute.internal nscd[28890]: 28890 disabled inotify-based monitoring for file `/etc/netgroup': No such file or directory
Jun 05 10:11:49 ip-172-31-7-21.eu-central-1.compute.internal nscd[28890]: 28890 stat failed for file `/etc/netgroup'; will try again later: No such file or directory
Jun 05 10:11:49 ip-172-31-7-21.eu-central-1.compute.internal nscd[28890]: 28890 Access Vector Cache (AVC) started
Jun 05 10:11:49 ip-172-31-7-21.eu-central-1.compute.internal systemd[1]: Started Name Service Cache Daemon.
Jun 05 10:12:08 ip-172-31-7-21.eu-central-1.compute.internal nscd[28890]: 28890 checking for monitored file `/etc/netgroup': No such file or directory
[root@ip-172-31-7-21 ~]# systemctl enable ntpd
Created symlink from /etc/systemd/system/multi-user.target.wants/ntpd.service to /usr/lib/systemd/system/ntpd.service.
[root@ip-172-31-7-21 ~]# systemctl start ntpd
[root@ip-172-31-7-21 ~]# systemctl status ntpd
? ntpd.service - Network Time Service
   Loaded: loaded (/usr/lib/systemd/system/ntpd.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2017-06-05 10:15:46 EDT; 5s ago
  Process: 29016 ExecStart=/usr/sbin/ntpd -u ntp:ntp $OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 29017 (ntpd)
   CGroup: /system.slice/ntpd.service
           +-29017 /usr/sbin/ntpd -u ntp:ntp -g

Jun 05 10:15:46 ip-172-31-7-21.eu-central-1.compute.internal ntpd[29017]: Listen and drop on 1 v6wildcard :: UDP 123
Jun 05 10:15:46 ip-172-31-7-21.eu-central-1.compute.internal ntpd[29017]: Listen normally on 2 lo 127.0.0.1 UDP 123
Jun 05 10:15:46 ip-172-31-7-21.eu-central-1.compute.internal ntpd[29017]: Listen normally on 3 eth0 172.31.7.21 UDP 123
Jun 05 10:15:46 ip-172-31-7-21.eu-central-1.compute.internal ntpd[29017]: Listen normally on 4 lo ::1 UDP 123
Jun 05 10:15:46 ip-172-31-7-21.eu-central-1.compute.internal ntpd[29017]: Listen normally on 5 eth0 fe80::46d:60ff:fe5a:439 UDP 123
Jun 05 10:15:46 ip-172-31-7-21.eu-central-1.compute.internal ntpd[29017]: Listening on routing socket on fd #22 for interface updates
Jun 05 10:15:46 ip-172-31-7-21.eu-central-1.compute.internal systemd[1]: Started Network Time Service.
Jun 05 10:15:46 ip-172-31-7-21.eu-central-1.compute.internal ntpd[29017]: 0.0.0.0 c016 06 restart
Jun 05 10:15:46 ip-172-31-7-21.eu-central-1.compute.internal ntpd[29017]: 0.0.0.0 c012 02 freq_set kernel 0.000 PPM
Jun 05 10:15:46 ip-172-31-7-21.eu-central-1.compute.internal ntpd[29017]: 0.0.0.0 c011 01 freq_not_set

```
```{r, engine='bash',  DB}
[root@ip-172-31-7-21 ~]# wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.42.tar.gz
[root@ip-172-31-7-21 ~]# tar -xzf ./mysql-connector-java-5.1.42.tar.gz
[root@ip-172-31-7-21 ~]# cd mysql-connector-java-5.1.42
[root@ip-172-31-7-21 mysql-connector-java-5.1.42]# sudo vi /etc/profile
			last line: export CLASSPATH=/home/ec2-user/mysql-connector-java-5.1.42/mysql-connector-java-5.1.42-bin.jar:$CLASSPATH
[root@ip-172-31-7-21 mysql-connector-java-5.1.42]# cd ~
[root@ip-172-31-7-21 ~]# sudo yum install mariadb-server -y
[root@ip-172-31-7-21 ~]# sudo systemctl start mariadb
[root@ip-172-31-7-21 ~]# sudo systemctl enable mariadb
[root@ip-172-31-7-21 ~]# /usr/bin/mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user.  If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n] Y
New password:
Re-enter new password:
Sorry, passwords do not match.

New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] Y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] Y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!
[root@ip-172-31-7-21 ~]# sudo vi /etc/my.cnf
[root@ip-172-31-7-21 ~]# cat /etc/my.cnf
[mysqld]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0
# Settings user and group are ignored when systemd is used.
# If you need to run mysqld under a different user or group,
# customize your systemd unit file for mariadb according to the
# instructions in http://fedoraproject.org/wiki/Systemd

[mysqld_safe]
log-error=/var/log/mariadb/mariadb.log
pid-file=/var/run/mariadb/mariadb.pid

#
# include all files from the config directory
#
!includedir /etc/my.cnf.d

[mysqld]
log-bin=mysql-bin
server-id=1 # or 2
bind-address=0.0.0.0

[root@ip-172-31-7-21 ~]# mysql -u root
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 3
Server version: 5.5.52-MariaDB MariaDB Server

Copyright (c) 2000, 2016, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> CREATE USER 'repl' IDENTIFIED BY '';
Query OK, 0 rows affected (0.01 sec)

MariaDB [(none)]> GRANT REPLICATION SLAVE ON *.* TO 'repl';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> SET GLOBAL binlog_format = 'ROW';
MariaDB [(none)]> FLUSH TABLES WITH READ LOCK;
MariaDB [(none)]> exit
Bye
[root@ip-172-31-7-21 ~]#


--On Replication client
[ec2-user@ip-172-31-15-237 ~]$ mysql -uroot -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 12
Server version: 5.5.52-MariaDB MariaDB Server

Copyright (c) 2000, 2016, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> CHANGE MASTER TO MASTER_HOST='52.59.220.8', MASTER_USER='rep', MASTER_PASSWORD='', MASTER_LOG_FILE='mysql-bin.000004', MASTER_LOG_POS=486;
Query OK, 0 rows affected (0.03 sec)

MariaDB [(none)]> exit
Bye
[ec2-user@ip-172-31-15-237 ~]$
--

--on EC2

https://stackoverflow.com/questions/9766014/connect-to-mysql-on-amazon-ec2-from-a-remote-server

There could be one of the following reasons:

You need make an entry in the Amazon Security Group to allow remote access from your machine to Amazon EC2 instance. :- I believe this is done by you as from your question it seems like you already made an entry with 0.0.0.0, which allows everybody to access the machine.

MySQL not allowing user to connect from remote machine:- By default MySql creates root user id with admin access. But root id's access is limited to localhost only. This means that root user id with correct password will not work if you try to access MySql from a remote machine. To solve this problem, you need to allow either the root user or some other DB user to access MySQL from remote machine. I would not recommend allowing root user id accessing DB from remote machine. You can use wildcard character % to specify any remote machine.

Check if machine's local firewall is not enabled. And if its enabled then make sure that port 3306 is open.


--on Master
mysql> SHOW MASTER STATUS;
mysql> GRANT REPLICATION SLAVE ON *.* TO 'user'@'FQDN' IDENTIFIED BY 'password';
mysql> SET GLOBAL binlog_format = 'ROW';
mysql> FLUSH TABLES WITH READ LOCK;

--on REPL
stop SLAVE;
CHANGE MASTER TO MASTER_HOST='52.59.220.8', MASTER_USER='repl', MASTER_PASSWORD='',MASTER_LOG_FILE='mysql-bin.000004', MASTER_LOG_POS=486;
START SLAVE;
SHOW SLAVE STATUS \G
--

```
```{r, engine='bash',  install CDH 5.8.3}
https://www.cloudera.com/documentation/enterprise/release-notes/topics/cdh_vd_cdh_download_58.html#cdh583

copy repo to /etc/yum.repos.d/ 
https://www.cloudera.com/documentation/enterprise/5-8-x/topics/cm_ig_install_path_b.html#concept_qyv_bt1_v5


[ec2-user@ip-172-31-7-21 yum.repos.d]$ sudo vi cloudera-manager.repo
[ec2-user@ip-172-31-7-21 yum.repos.d]$ sudo cat cloudera-manager.repo                                                [cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 7 x86_64
name=Cloudera Manager
#baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5/
baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.8.3/
gpgkey =https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1

[ec2-user@ip-172-31-7-21 yum.repos.d]$ sudo yum clean all
[ec2-user@ip-172-31-7-21 yum.repos.d]$ sudo yum install cloudera-manager-agent -y 
[ec2-user@ip-172-31-7-21 yum.repos.d]$ sudo yum install cloudera-manager-daemons cloudera-manager-server -y
Starting cloudera-scm-agent (via systemctl):               [  OK  ]

#Disable SELinux Temporarily
#To disable SELinux temporarily, issue the command below as root:
echo 0 > /selinux/enforce
#Alternatively, you can use the setenforce tool as follows:
setenforce 0
#Else, use the Permissive option instead of 0 as below:
setenforce Permissive

[root@ip-172-31-8-243 yum.repos.d]# sestatus

[root@ip-172-31-8-243 share]  sudo mkdir -p /usr/share/java/
[root@ip-172-31-8-243 share]# sudo cp ~/mysql-connector-java-5.1.42/mysql-connector-java-5.1.42-bin.jar /usr/share/java/mysql-connector-java.jar

[root@ip-172-31-8-243 share]# mysql -u root -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 7
Server version: 5.5.52-MariaDB MariaDB Server

Copyright (c) 2000, 2016, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> CREATE DATABASE cmserver DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> GRANT ALL on cmserver.* TO 'cmserveruser'@'%' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> CREATE DATABASE metastore DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> CREATE DATABASE hive DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> GRANT ALL on metastore.* TO 'hiveuser'@'%' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> CREATE DATABASE amon DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> GRANT ALL on amon.* TO 'amonuser'@'%' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> CREATE DATABASE rman DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> GRANT ALL on rman.* TO 'rmanuser'@'%' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> CREATE DATABASE oozie DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> GRANT ALL on oozie.* TO 'oozieuser'@'%' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> CREATE DATABASE hue DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> GRANT ALL on hue.* TO 'hueuser'@'%' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> exit
Bye

[root@ip-172-31-8-243 share]# sudo /usr/share/cmf/schema/scm_prepare_database.sh mysql cmserver cmserveruser password
JAVA_HOME=/usr/java/jdk1.7.0_60
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.7.0_60/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
[                          main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!
[ec2-user@ip-172-31-7-21 ~]$  sudo service cloudera-scm-agent start
[root@ip-172-31-8-243 share]# sudo service cloudera-scm-server start

--> Ports

--> http://52.59.196.39:7180/
```
```{r, engine='bash',  lokal repo}
[root@ip-172-31-8-243 ~]# mkdir /var/www/html/cdh5.8.3
[root@ip-172-31-8-243 ~]# cd /var/www/html/cdh5.8.3
[root@ip-172-31-8-243 cdh5.8.3]# wget http://archive.cloudera.com/cdh5/parcels/5.8.3/manifest.json
--2017-06-06 10:21:55--  http://archive.cloudera.com/cdh5/parcels/5.8.3/manifest.json
Resolving archive.cloudera.com (archive.cloudera.com)... 151.101.12.167
Connecting to archive.cloudera.com (archive.cloudera.com)|151.101.12.167|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 63718 (62K) [application/json]
Saving to: ‘manifest.json’

100%[===================================================================================================================================================================================================>] 63,718      --.-K/s   in 0.08s

2017-06-06 10:21:55 (785 KB/s) - ‘manifest.json’ saved [63718/63718]

[root@ip-172-31-8-243 cdh5.8.3]# wget http://archive.cloudera.com/cdh5/parcels/5.8.3/CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel
--2017-06-06 10:22:13--  http://archive.cloudera.com/cdh5/parcels/5.8.3/CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel
Resolving archive.cloudera.com (archive.cloudera.com)... 151.101.12.167
Connecting to archive.cloudera.com (archive.cloudera.com)|151.101.12.167|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1479696719 (1.4G)
Saving to: ‘CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel’

34% [==================================================================>                                                                                                                                 ] 509,178,865 39.0MB/s  eta 19s    g37% [=========================================================================>                                                                                                                          ] 560,389,261 36.2MB/s  eta 18s    h100%[=================================================================================================================================================================================================>] 1,479,696,719 45.2MB/s   in 29s

2017-06-06 10:22:42 (48.8 MB/s) - ‘CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel’ saved [1479696719/1479696719]

[root@ip-172-31-8-243 cdh5.8.3]# wget http://archive.cloudera.com/cdh5/parcels/5.8.3/CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel.sha1
--2017-06-06 10:23:24--  http://archive.cloudera.com/cdh5/parcels/5.8.3/CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel.sha1
Resolving archive.cloudera.com (archive.cloudera.com)... 151.101.12.167
Connecting to archive.cloudera.com (archive.cloudera.com)|151.101.12.167|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 41 [application/x-sha1]
Saving to: ‘CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel.sha1’

100%[===================================================================================================================================================================================================>] 41          --.-K/s   in 0s

2017-06-06 10:23:24 (7.27 MB/s) - ‘CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel.sha1’ saved [41/41]

[root@ip-172-31-8-243 cdh5.8.3]# ls -la
total 1445092
drwxr-xr-x. 2 root root       4096 Jun  6 10:23 .
drwxr-xr-x. 3 root root         21 Jun  6 10:21 ..
-rw-r--r--. 1 root root 1479696719 Oct 27  2016 CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel
-rw-r--r--. 1 root root         41 Oct 27  2016 CDH-5.8.3-1.cdh5.8.3.p0.2-el7.parcel.sha1
-rw-r--r--. 1 root root      63718 Oct 27  2016 manifest.json
[root@ip-172-31-8-243 cdh5.8.3]# chmod -R ugo+rX /var/www/html/cdh5.8.3/
[root@ip-172-31-8-243 cdh5.8.3]# systemctl status httpd
? httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
     Docs: man:httpd(8)
           man:apachectl(8)
[root@ip-172-31-8-243 cdh5.8.3]# systemctl start httpd
[root@ip-172-31-8-243 cdh5.8.3]# systemctl status httpd
? httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
   Active: active (running) since Tue 2017-06-06 10:26:21 EDT; 1s ago
     Docs: man:httpd(8)
           man:apachectl(8)
 Main PID: 29697 (httpd)
   Status: "Processing requests..."
   CGroup: /system.slice/httpd.service
           +-29697 /usr/sbin/httpd -DFOREGROUND
           +-29698 /usr/sbin/httpd -DFOREGROUND
           +-29699 /usr/sbin/httpd -DFOREGROUND
           +-29700 /usr/sbin/httpd -DFOREGROUND
           +-29701 /usr/sbin/httpd -DFOREGROUND
           +-29702 /usr/sbin/httpd -DFOREGROUND

Jun 06 10:26:21 ip-172-31-8-243.eu-central-1.compute.internal systemd[1]: Starting The Apache HTTP Server...
Jun 06 10:26:21 ip-172-31-8-243.eu-central-1.compute.internal systemd[1]: Started The Apache HTTP Server.
[root@ip-172-31-8-243 cdh5.8.3]# systemctl status httpd
? httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
   Active: active (running) since Tue 2017-06-06 10:26:21 EDT; 13s ago
     Docs: man:httpd(8)
           man:apachectl(8)
 Main PID: 29697 (httpd)
   Status: "Total requests: 1; Current requests/sec: 0.111; Current traffic:   0 B/sec"
   CGroup: /system.slice/httpd.service
           +-29697 /usr/sbin/httpd -DFOREGROUND
           +-29698 /usr/sbin/httpd -DFOREGROUND
           +-29699 /usr/sbin/httpd -DFOREGROUND
           +-29700 /usr/sbin/httpd -DFOREGROUND
           +-29701 /usr/sbin/httpd -DFOREGROUND
           +-29702 /usr/sbin/httpd -DFOREGROUND
           +-29705 /usr/sbin/httpd -DFOREGROUND
           +-29707 /usr/sbin/httpd -DFOREGROUND

Jun 06 10:26:21 ip-172-31-8-243.eu-central-1.compute.internal systemd[1]: Starting The Apache HTTP Server...
Jun 06 10:26:21 ip-172-31-8-243.eu-central-1.compute.internal systemd[1]: Started The Apache HTTP Server.
[root@ip-172-31-8-243 cdh5.8.3]#

CREATE USER 'amonuser'@'aws1' IDENTIFIED BY 'password';
CREATE USER 'amonuser'@'aws2' IDENTIFIED BY 'password';
CREATE USER 'amonuser'@'aws3' IDENTIFIED BY 'password';
CREATE USER 'amonuser'@'aws4' IDENTIFIED BY 'password';
CREATE USER 'amonuser'@'aws5' IDENTIFIED BY 'password';

CREATE USER 'rmanuser'@'aws1' IDENTIFIED BY 'password';
CREATE USER 'rmanuser'@'aws2' IDENTIFIED BY 'password';
CREATE USER 'rmanuser'@'aws3' IDENTIFIED BY 'password';
CREATE USER 'rmanuser'@'aws4' IDENTIFIED BY 'password';
CREATE USER 'rmanuser'@'aws5' IDENTIFIED BY 'password';

CREATE USER 'oozieuser'@'aws1' IDENTIFIED BY 'password';
CREATE USER 'oozieuser'@'aws2' IDENTIFIED BY 'password';
CREATE USER 'oozieuser'@'aws3' IDENTIFIED BY 'password';
CREATE USER 'oozieuser'@'aws4' IDENTIFIED BY 'password';
CREATE USER 'oozieuser'@'aws5' IDENTIFIED BY 'password';

CREATE USER 'hiveuser'@'aws1' IDENTIFIED BY 'password';
CREATE USER 'hiveuser'@'aws2' IDENTIFIED BY 'password';
CREATE USER 'hiveuser'@'aws3' IDENTIFIED BY 'password';
CREATE USER 'hiveuser'@'aws4' IDENTIFIED BY 'password';
CREATE USER 'hiveuser'@'aws5' IDENTIFIED BY 'password';

CREATE USER 'hueuser'@'aws1' IDENTIFIED BY 'password';
CREATE USER 'hueuser'@'aws2' IDENTIFIED BY 'password';
CREATE USER 'hueuser'@'aws3' IDENTIFIED BY 'password';
CREATE USER 'hueuser'@'aws4' IDENTIFIED BY 'password';
CREATE USER 'hueuser'@'aws5' IDENTIFIED BY 'password';

##--------------

CREATE USER 'amonuser'@'ec2-52-59-196-39.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'amonuser'@'ec2-54-93-222-31.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'amonuser'@'ec2-54-93-119-59.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'amonuser'@'ec2-52-59-237-208.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'amonuser'@'ec2-52-59-246-54.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';

CREATE USER 'rmanuser'@'ec2-52-59-196-39.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'rmanuser'@'ec2-54-93-222-31.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'rmanuser'@'ec2-54-93-119-59.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'rmanuser'@'ec2-52-59-237-208.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'rmanuser'@'ec2-52-59-246-54.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';

CREATE USER 'oozieuser'@'ec2-52-59-196-39.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'oozieuser'@'ec2-54-93-222-31.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'oozieuser'@'ec2-54-93-119-59.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'oozieuser'@'ec2-52-59-237-208.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'oozieuser'@'ec2-52-59-246-54.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';

CREATE USER 'hiveuser'@'ec2-52-59-196-39.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'hiveuser'@'ec2-54-93-222-31.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'hiveuser'@'ec2-54-93-119-59.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'hiveuser'@'ec2-52-59-237-208.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'hiveuser'@'ec2-52-59-246-54.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';

CREATE USER 'hueuser'@'ec2-52-59-196-39.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'hueuser'@'ec2-54-93-222-31.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'hueuser'@'ec2-54-93-119-59.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'hueuser'@'ec2-52-59-237-208.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';
CREATE USER 'hueuser'@'ec2-52-59-246-54.eu-central-1.compute.amazonaws.com' IDENTIFIED BY 'password';


##--------------

CREATE USER 'amonuser'@'52.59.196.39' IDENTIFIED BY 'password';
CREATE USER 'amonuser'@'54.93.222.31' IDENTIFIED BY 'password';
CREATE USER 'amonuser'@'54.93.119.59' IDENTIFIED BY 'password';
CREATE USER 'amonuser'@'52.59.237.208' IDENTIFIED BY 'password';
CREATE USER 'amonuser'@'52.59.246.54' IDENTIFIED BY 'password';

CREATE USER 'rmanuser'@'52.59.196.39' IDENTIFIED BY 'password';
CREATE USER 'rmanuser'@'54.93.222.31' IDENTIFIED BY 'password';
CREATE USER 'rmanuser'@'54.93.119.59' IDENTIFIED BY 'password';
CREATE USER 'rmanuser'@'52.59.237.208' IDENTIFIED BY 'password';
CREATE USER 'rmanuser'@'52.59.246.54' IDENTIFIED BY 'password';

CREATE USER 'oozieuser'@'52.59.196.39' IDENTIFIED BY 'password';
CREATE USER 'oozieuser'@'54.93.222.31' IDENTIFIED BY 'password';
CREATE USER 'oozieuser'@'54.93.119.59' IDENTIFIED BY 'password';
CREATE USER 'oozieuser'@'52.59.237.208' IDENTIFIED BY 'password';
CREATE USER 'oozieuser'@'52.59.246.54' IDENTIFIED BY 'password';

CREATE USER 'hiveuser'@'52.59.196.39' IDENTIFIED BY 'password';
CREATE USER 'hiveuser'@'54.93.222.31' IDENTIFIED BY 'password';
CREATE USER 'hiveuser'@'54.93.119.59' IDENTIFIED BY 'password';
CREATE USER 'hiveuser'@'52.59.237.208' IDENTIFIED BY 'password';
CREATE USER 'hiveuser'@'52.59.246.54' IDENTIFIED BY 'password';

CREATE USER 'hueuser'@'52.59.196.39' IDENTIFIED BY 'password';
CREATE USER 'hueuser'@'54.93.222.31' IDENTIFIED BY 'password';
CREATE USER 'hueuser'@'54.93.119.59' IDENTIFIED BY 'password';
CREATE USER 'hueuser'@'52.59.237.208' IDENTIFIED BY 'password';
CREATE USER 'hueuser'@'52.59.246.54' IDENTIFIED BY 'password';
```
