참고사이트 :  
https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html  
http://blog.naver.com/PostView.nhn?blogId=complusblog&logNo=220974258517&beginTime=0&jumpingVid=&from=search&redirect=Log&widgetTypeCall=true  

### docker 생성하기
https://hub.docker.com/ --> registry 등록  

### 리눅스에 도커 설치하기
- script로 설치 (루트권한 요구됨)  
$ curl -fsSL https://get.docker.com/ | sudo sh  
![image](https://user-images.githubusercontent.com/56099627/89248549-fe43c680-d64a-11ea-87e9-15ece01f95b8.png)  
- 버전 확인 $ docker version  
![image](https://user-images.githubusercontent.com/56099627/89249042-21bb4100-d64c-11ea-96f9-63840894d615.png)  
- docker 라는 유저그룹 생성  
$ cat /etc/group | grep docker  
![image](https://user-images.githubusercontent.com/56099627/89250225-3947f900-d64f-11ea-8f49-1698ad2ba3ec.png)  
- docker에 사용자 등록 해주기  
$ sudo usermod -a -G docker <USER_ID>  
$ sudo usermod -a -G docker jimin 
![image](https://user-images.githubusercontent.com/56099627/89253996-13bfed00-d659-11ea-983f-d8b7cbcb6840.png)  
- 버전확인 했을 시, **Error: got permission denied while trying to connect to the docker daemon socket** 해결은 $ sudo chmod 666 /var/run/docker.sock 실행하기  
![image](https://user-images.githubusercontent.com/56099627/89254188-8af58100-d659-11ea-9b6b-4d959ea29681.png)  

