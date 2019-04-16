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



sudo sysctl -w vm.swappiness=1

#### se linux disable
sudo vi /etc/selinux/config
change ->SELINUX=disabled

#### disabled hugepage support
sudo vi /etc/rc.d/rc.local
add
echo "never" >/sys/kernel/nm/transparent_
sudo chmod +x /etc/rc.d/rc.local
sudo vi /ect/default/grub
 add -> trans
 grub2-mkconfig

### Install a supported Oracle JDK on your first node
sudo yum install java-1.8.0-openjdk

### Install a supported JDBC connector on all nodes
### Create the databases and access grants you will need
### Configure Cloudera Manager to connect to the database
### Start your Cloudera Manager server -- debug as necessary
### Do not continue until you can browse your CM instance at port 7180





ns/swich/conf
