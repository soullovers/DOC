### AWS EC2의 .pem 파일로 서버 인스턴스에 접속하기
https://m.blog.naver.com/PostView.nhn?blogId=alice_k106&logNo=220882708567&proxyReferer=https%3A%2F%2Fwww.google.com%2F
centos


aws cm install
### udpate yum
```
sudo yum update
sudo yum install -y wget
sudo -i
```
### add ec2-user to suusers
```
sudo passwd centos
sudo vi /etc/ssh/sshd_config
```
change ->
| PasswordAuthentication yes
```
sudo systemctl restart sshd.service
```
```
sudo visudo 
```
add -> 
| centos ALL=(ALL) ALL

### change the run level to multi-user text mode
```
sudo systemctl get-default
sudo systemctl set-default multi-user.target
```

### disable firewall
```
sudo systemctl disable firewalld
sudo systemctl status firewalld
```

## change vm.swappiness
```
sudo sysctl -w vm.swappiness=1
```

#### se linux disable
```
sudo vi /etc/selinux/config
```
change -> 
| SELINUX=disabled


#### disabled hugepage support
```
sudo vi /etc/rc.d/rc.local
```
add -> 

| echo "never" > /sys/kernel/mm/transparent_hugepage/enabled
| echo "never" > /sys/kernel/mm/transparent_hugepage/defrag
```
sudo chmod +x /etc/rc.d/rc.local
sudo vi /etc/default/grub
```
 add -> 
 | transparent_hugepage=naver (ON line GRUB_CMDLINE_LINUX)
 
 ``` 
 grub2-mkconfig -o /boot/grub2/grub.cfg
 sudo systemctl start tuned
 sudo tuned-adm off
 sudo tuned-adm list
 sudo systemctl stop tuned
 sudo systemctl disable tuned
 ```
 ### check to see tahat ntp service is running
 ```
sudo systemctl stop chronyd
sudo systemctl disable chronyd
sudo yum -y install ntp
sudo systemctl enable ntpd.service
sudo systemctl start ntpd.service
sudo hwclock --systohc
sudo systemctl status ntpd.service
```

yum clean all  

### Install a supported Oracle JDK on your first node
```
sudo yum install java-1.8.0-openjdk
```
Some RHEL 7 AMIs do not include wget by default. If your RHEL AMI does not include wget, install it now:
```
sudo yum install wget
```
Add the Altus Director repository to the package manager:
```
cd /etc/yum.repos.d/
sudo wget "http://archive.cloudera.com/director6/6.1/redhat7/cloudera-director.repo"
```
Install Altus Director server and client by running the following command:
```
sudo yum install cloudera-director-server cloudera-director-client
```

### Install a supported JDBC connector on all nodes
- mysql JDBC Connector 설치
```
sudo systemctl stop mariadb
```
vi /etc/my.cnf
```
[mysqld]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
transaction-isolation = READ-COMMITTED
# Disabling symbolic-links is recommended to prevent assorted security risks;
# to do so, uncomment this line:
symbolic-links = 0
# Settings user and group are ignored when systemd is used.
# If you need to run mysqld under a different user or group,
# customize your systemd unit file for mariadb according to the
# instructions in http://fedoraproject.org/wiki/Systemd

key_buffer = 16M
key_buffer_size = 32M
max_allowed_packet = 32M
thread_stack = 256K
thread_cache_size = 64
query_cache_limit = 8M
query_cache_size = 64M
query_cache_type = 1

max_connections = 550
#expire_logs_days = 10
#max_binlog_size = 100M

#log_bin should be on a disk with enough free space.
#Replace '/var/lib/mysql/mysql_binary_log' with an appropriate path for your
#system and chown the specified folder to the mysql user.
log_bin=/var/lib/mysql/mysql_binary_log

#In later versions of MariaDB, if you enable the binary log and do not set
#a server_id, MariaDB will not start. The server_id must be unique within
#the replicating group.
server_id=1

binlog_format = mixed

read_buffer_size = 2M
read_rnd_buffer_size = 16M
sort_buffer_size = 8M
join_buffer_size = 8M

# InnoDB settings
innodb_file_per_table = 1
innodb_flush_log_at_trx_commit  = 2
innodb_log_buffer_size = 64M
innodb_buffer_pool_size = 4G
innodb_thread_concurrency = 8
innodb_flush_method = O_DIRECT
innodb_log_file_size = 512M

[mysqld_safe]
log-error=/var/log/mariadb/mariadb.log
pid-file=/var/run/mariadb/mariadb.pid

#
# include all files from the config directory
#
!includedir /etc/my.cnf.d
```
#### Ensure the MariaDB server starts at boot:
sudo systemctl enable mariadb

##### Start the MariaDB server:
sudo systemctl enable mariadb

#### Run /usr/bin/mysql_secure_installation to set the MariaDB root password and other security-related setting
```
sudo /usr/bin/mysql_secure_installation
[...]
Enter current password for root (enter for none):
OK, successfully used password, moving on...
[...]
Set root password? [Y/n] Y
New password:
Re-enter new password:
[...]
Remove anonymous users? [Y/n] Y
[...]
Disallow root login remotely? [Y/n] N
[...]
Remove test database and access to it [Y/n] Y
[...]
Reload privilege tables now? [Y/n] Y
[...]
All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.
```

Thanks for using MariaDB!

#### error발생시 링크생성
ln -s /tmp/mysql.sock /var/lib/mysql/mysql.sock



### Create the databases and access grants you will need
sudo systemctl stop mariadb
### Configure Cloudera Manager to connect to the database
### Start your Cloudera Manager server -- debug as necessary
### Do not continue until you can browse your CM instance at port 7180
```
sudo wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.15.2/ -P /etc/yum.repos.d/
sudo rpm --import https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
```


ns/swich/conf
