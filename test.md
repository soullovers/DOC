### AWS EC2의 .pem 파일로 서버 인스턴스에 접속하기
https://m.blog.naver.com/PostView.nhn?blogId=alice_k106&logNo=220882708567&proxyReferer=https%3A%2F%2Fwww.google.com%2F
centos


aws cm install
### udpate yum
sudo yum update
sudo yum install -y wget
sudo -i

### add ec2-user to suusers
sudo passwd centos
sudo vi /etc/ssh/sshd_config
change ->
PasswordAuthentication yes
sudo systemctl restart sshd.service

sudo visudo 
add -> centos ALL=(ALL) ALL

### change the run level to multi-user text mode
sudo systemctl get-default
sudo systemctl set-default multi-user.target


### disable firewall
sudo systemctl disable firewalld
sudo systemctl status firewalld


## change vm.swappiness
```
sudo sysctl -w vm.swappiness=1
```

#### se linux disable
sudo vi /etc/selinux/config
change -> 
```
     SELINUX=disabled
 ```

#### disabled hugepage support
```
sudo vi /etc/rc.d/rc.local
```
add -> 
```
echo "never" > /sys/kernel/mm/transparent_hugepage/enabled
echo "never" > /sys/kernel/mm/transparent_hugepage/defrag
```
sudo chmod +x /etc/rc.d/rc.local
sudo vi /etc/default/grub
 add -> transparent_hugepage=naver (ON line GRUB_CMDLINE_LINUX)
 grub2-mkconfig -o /boot/grub2/grub.cfg
 ```
 sudo systemctl start tuned
 sudo tuned-adm off
 sudo tuned-adm list
 sudo systemctl stop tuned
 sudo systemctl disable tuned
 ```
 ### check to see tahat ntp service is running
sudo systemctl stop chronyd
sudo systemctl disable chronyd
sudo yum -y install ntp
sudo systemctl enable ntpd.service
sudo systemctl start ntpd.service
sudo hwclock --systohc
sudo systemctl status ntpd.service

### Install a supported Oracle JDK on your first node
sudo yum install java-1.8.0-openjdk

### Install a supported JDBC connector on all nodes
- mysql JDBC Connector 설치
```
wget http://www.java2s.com/Code/JarDownload/mysql/mysql-connector-java-commercial-5.1.7-bin.jar.zip
unzip mysql-connector-java-commercial-5.1.7-bin.jar.zip
cp mysql-connector-java-commercial-5.1.7-bin.jar  $HIVE_HOME/lib/
```
### Create the databases and access grants you will need
### Configure Cloudera Manager to connect to the database
### Start your Cloudera Manager server -- debug as necessary
### Do not continue until you can browse your CM instance at port 7180

sudo wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.15.2/ -P /etc/yum.repos.d/
sudo rpm --import https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera



ns/swich/conf
