https://blog.lael.be/post/8404  

### vsftpd 설치 
0. 터미널에 들어가서 관리자 권한으로 실행을 해둠  
1. 설치 전 파일 목록 업데이트 $ apt update  
2. vsftpd 설치 패키지가 존재하는지 확인 $ apt search vsftpd  
![image](https://user-images.githubusercontent.com/56099627/98206458-468dc000-1f7d-11eb-9977-46ce3e2b5293.png)  
--> 존재하고 있음을 확인함  
"vsftpd/bionic 3.0.3-9build1 amd64 : lightweight, efficient FTP server written for security"  
3. vsftp 설치  
$ sudo apt install vsftpd  
vsftpd 프로그램이 설치되고, 서비스에 등록되고, 실행된다  
![image](https://user-images.githubusercontent.com/56099627/98206753-ccaa0680-1f7d-11eb-81fa-d35dfdefe2bf.png)  
4. vsftpd 실행 상태 확인  
$ service vsftpd status  
![image](https://user-images.githubusercontent.com/56099627/98206959-3a563280-1f7e-11eb-8d26-650f2c9dc15b.png)  
5. 네트워크 포트 확인  
$ netstat -natp | grep ftp  
(만약에 netstat가 없다고 한다면 **sudo apt install net-tools** 설치하기)  
![image](https://user-images.githubusercontent.com/56099627/98207528-28c15a80-1f7f-11eb-916a-39c321abea61.png)  
--> vsftpd 가 실행중이며 TCP 21 번 포트로 LISTEN 중...  
6. vsftpd 환경설정  
$ sudo vim /etc/vsftpd.conf  
```
listen=YES
listen_ipv6=NO
anonymous_enable=NO
port_enable=NO
pasv_enable=YES
local_enable=YES
write_enable=YES
use_localtime=YES
xferlog_enable=YES
chroot_local_user=YES
allow_writeable_chroot=YES
secure_chroot_dir=/var/run/vsftpd/empty
pam_service_name=vsftpd
ftpd_banner=Welcome to My FTP Server!
ssl_enable=YES
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
listen_port=21
pasv_min_port=60020
pasv_max_port=60030
#utf8_filesystem=YES
#local_umask=022
```
7. 재시작  
$ service vsftpd restart  

(참고) 이 서버에서 연결가능한 포트번호 보기  
$ netstat -natp | grep LISTEN  
![image](https://user-images.githubusercontent.com/56099627/98207803-93729600-1f7f-11eb-997c-59d8182afd28.png)  

### filezila 설치
1. 터미널에서 명령어으로 설치  
(생략가능)$ sudo apt-get update  
$ sudo apt-get install filezilla  
![image](https://user-images.githubusercontent.com/56099627/98220342-7e9efe00-1f91-11eb-924a-fdcf5523afed.png)  
2. 프로그램 리스트에서 ui 확인  
![image](https://user-images.githubusercontent.com/56099627/98220536-c45bc680-1f91-11eb-838e-2486d7fe453c.png)  
