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
1. https://hub.docker.com/r/nvidia/cuda/tags/ 에 들어가서 원하는 버전 선택하여 컨테이너 이미지 다운로드 하기
2. 아래의 명령어는 CUDA Toolkit 10.2 버전의 컨테이너 이미지를 다운 받고($ docker pull nvidia/cuda:10.2-base), nvidia-smi 명령어를 실행한 예제  
$ docker run --gpus all nvidia/cuda:10.2-base nvidia-smi 
/bin/bash 명령어를 실행한 예제  
$ docker run --rm -it nvidia/cuda:10.2-base /bin/bash
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
2. docker 실행 서비스에서 설정변경 & Docker 프로세스 중지  
/lib/systemd/system/docker.service 파일을 열고 아래 내용을 수정한다.  
#ExecStart=/usr/bin/dockerd -H fd://  
ExecStart=/usr/bin/dockerd -g /home/ykkim/docker -H fd://  
수정이 되면 도커를 중지시킨다.  
$ sudo systemctl stop docker  
$ sudo systemctl daemon-reload  
![image](https://user-images.githubusercontent.com/56099627/90723669-293f4300-e2f8-11ea-8c16-ea2c6bc7b225.png)  
3. Docker NEW 저장 경로 만들기 & NEW 경로로 Docker 복제  
도커 데이터가 저장될 경로를 먼저 만들어주어야 한다.  
$ mkdir /home/ykkim/docker  
그런 다음 기존에 docker 경로를 위 경로로 통째로 복제해준다.  
$ sudo rsync -aqxP /var/lib/docker /home/ykkim/docker  
4. 마지막 이제 도커를 실행  
$ sudo systemctl start docker  

### sudo service docker stop 후 다시 접속 하고 자 할때 
**issue: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?**
https://velog.io/@pop8682/Docker-Cannot-connect-to-the-Docker-daemon-at-unixvarrundocker.sock.-Is-the-docker-daemon-running-%EC%97%90%EB%9F%AC-%ED%95%B4%EA%B2%B0  
- 해결 방안  
간단하게 정리하자면 Docker daemon을 돌려주기만 하면된다.  
방금처럼 dockerd를 매번 실행하기는 번거러우니 아래 두 라인을 도커 설치 이후 입력하면 편할 것이다.  
$ systemctl start docker  
docker를 daemon으로 실행하라는 명령어로 dockerd와 같지만 로그없이 실행한다고 보면 편하다  
$ systemctl enable docker  
컴퓨터가 새로 시작하거나 부팅시 자동으로 docker daemon을 실행하라는 명령어이다.  
![image](https://user-images.githubusercontent.com/56099627/90713572-98a93880-e2e0-11ea-81e9-c831996d0c45.png)  

### docker image 지울때 에러
https://nirsa.tistory.com/61  
**Error response from daemon: conflict: unable to remove repository reference "python:latest" (must force) - container 01715923a951 is using its referenced image 4e2d08f34f6d**  
- 문제 발생
![image](https://user-images.githubusercontent.com/56099627/90725811-af10bd80-e2fb-11ea-9b52-f6d45f974ae8.png)  
해당 에러는 이미지 busy box를 삭제 할 때에 어떠한 컨테이너가 이미 삭제할 이미지를 참조중이기 때문에(컨테이너의 실행 유무는 상관없이) 발생하는 에러 
해당 ID 를 가진 컨테이너를 확인 $ docker container ls -a  
python:latest (이미지)는 컨테이너 ID 01715923a951을 가지고 있습니다. 잘 보시면 IMAGE 필드에 삭제하려는 busybox를 바라보고 있는 컨테이너들이 있는데, 결국 이 **컨테이너을 모두 삭제해주어야 이미지를 삭제할 수 있음**  
도커 이미지 삭제 $ docker rmi [IMAGE ID 혹은 REPOSITORY:TAG]  
컨테이너 ID 삭제 $ docker rm [NAME]  
- 결과 확인  
![image](https://user-images.githubusercontent.com/56099627/90726382-9654d780-e2fc-11ea-9572-c37e07ae0dcf.png)  
