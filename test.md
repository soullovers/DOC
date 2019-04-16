### AWS EC2의 .pem 파일로 서버 인스턴스에 접속하기
https://m.blog.naver.com/PostView.nhn?blogId=alice_k106&logNo=220882708567&proxyReferer=https%3A%2F%2Fwww.google.com%2F
centos


aws cm install
### udpate yum
sudo yum update
sudo yum install -y wget


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
