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
$ sudo usermod -aG docker <USER_ID>  
$ sudo usermod -aG docker jimin 
![image](https://user-images.githubusercontent.com/56099627/89253996-13bfed00-d659-11ea-983f-d8b7cbcb6840.png)  
- 버전확인 했을 시, **Error: got permission denied while trying to connect to the docker daemon socket** 해결은 $ sudo chmod 666 /var/run/docker.sock 실행하기  
(참고: https://github.com/palantir/gradle-docker/issues/188 )
![image](https://user-images.githubusercontent.com/56099627/89254188-8af58100-d659-11ea-9b6b-4d959ea29681.png)  

### nvidia docker 설치하기  
https://hiseon.me/linux/ubuntu/install-docker/  
https://hub.docker.com/r/nvidia/cuda/tags/  
- 도커에 nvidia toolkit 10.2 설치  
$ docker run --gpus all nvidia/cuda:10.2-base nvidia-smi  
![image](https://user-images.githubusercontent.com/56099627/89255755-6bf8ee00-d65d-11ea-949b-4f00751ae892.png)  

### docker 이미지 레파지토리에 올리고 삭제하기
- 레파지토리 로그인 하기  
![image](https://user-images.githubusercontent.com/56099627/89258912-1a079680-d664-11ea-95ee-2e2cac7a6466.png)  
- 로컬 이미지에 태그 설정 & 이미지 올리기  
$ docker tag <업로드할 이미지의 ID> <이용자ID>/<생성된 리파지토리 이름>:<임의의 태그이름>  
$ docker tag 69ba6d511482 hihijimin/dockerlab:base  
이미지 올리기 $ docker push hihijimin/dockerlab:base  
![image](https://user-images.githubusercontent.com/56099627/89259251-dbbea700-d664-11ea-9e84-1aab87a9af62.png)  
- 이미지 삭제  
![image](https://user-images.githubusercontent.com/56099627/89259713-dca40880-d665-11ea-8bbc-8de8ca648c9b.png)  

### docker 실행
```
--rm: 프로세스 종료시 컨테이너 자동 제거, -it: -i와 -t을 동시에 사용한것임 터미널 입력을 위한 옵션(컨테이너의 표준 입력과 로컬 컴퓨터의 키보드 입력을 연결)
```
- nvidia/cuda:10.2 실행  
도커 일회성으로 접속 하기 $ docker run --rm -it nvidia/cuda:10.2-base  
도커 접속 하기 $ docker run -it nvidia/cuda:10.2-base  
- local 경로와 docker의 nvidia/cuda:10.2 에 연결? 하여 실행  
$ docker run --rm -it -v /media/jimin/D/project:/project  nvidia/cuda:10.2-base  
![image](https://user-images.githubusercontent.com/56099627/89272044-8a201780-d678-11ea-97e6-09de7e65e085.png)  
- python image 설치 & 실행  
$ docker run -it python  
![image](https://user-images.githubusercontent.com/56099627/89280062-12a3b580-d683-11ea-9a35-e796dcbccabe.png)  

### nvidia-docker 개발환경 셋팅
참고: https://jybaek.tistory.com/791  
1. 컨테이너 접속 하기  
(일회성을 접속하지 않기 위해 --rm 빼기)  
![image](https://user-images.githubusercontent.com/56099627/90592528-bf079f00-e220-11ea-99ec-b880c44cb70c.png)  
2. sources.list 셋팅 필수 패키지를 설치  
- sources.list 셋팅(기본적인 필요한 패키지를 다운로드 하기 위해)  
$ sed -i 's/archive.ubuntu.com/ftp.daumkakao.com/g' /etc/apt/sources.list  
$ apt-get update  
$ apt-get dist-upgrade -y  
- 위 셋팅이 끝났으면 필수 패키지를 설치한다  
$ apt-get install -y wget vim git gcc  build-essential  
![image](https://user-images.githubusercontent.com/56099627/90592623-fbd39600-e220-11ea-85a6-fd372f655007.png)  
3. ananconda 설치  
$ wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh  
$ bash Anaconda3-2020.07-Linux-x86_64.sh  
![image](https://user-images.githubusercontent.com/56099627/90592994-e14dec80-e221-11ea-8ebf-6992ceadb8d5.png)  

### 자주 들어가는 docker-container 접속
1. 새로운 container 만들기  
$ docker run -it [container ID 혹은 names]  
- container 이름 변경 : $ docker rename [컨테이너 이름] [바꾸고자 하는 컨테이너 이름]  
- container 삭제 : $ docker rm [컨테이너 이름]  
2. 만든 container에 다시 접속  
실행 가능한 컨테이너 확인 $ docker ps  
$ docker start [컨테이너 이름]  
$ docker attach [컨테이너 이름]  

### docker 저장위치 변경
https://yookeun.github.io/docker/2018/10/29/docker-change/  
http://dveamer.github.io/backend/DockerImageDirectory.html  
1. 위치 변경 전 확인(꼭 sudo로 해야함)  
$ sudo lsof | grep /var/lib/docker  
'/var/lib/docker' 디렉토리에 위치한 여러파일들을 dockerd, docker-co 프로세스들이 사용중인 것을 확인할 수 있음  
![image](https://user-images.githubusercontent.com/56099627/90712640-731b2f80-e2de-11ea-8d74-336d43aecb33.png)  
2. Docker 프로세스 중지  
$ sudo service docker stop  
![image](https://user-images.githubusercontent.com/56099627/90712828-d6a55d00-e2de-11ea-8914-25265d9b22b1.png)
3. 
