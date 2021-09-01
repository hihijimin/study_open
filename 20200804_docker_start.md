참고사이트 :  
https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html  
http://blog.naver.com/PostView.nhn?blogId=complusblog&logNo=220974258517&beginTime=0&jumpingVid=&from=search&redirect=Log&widgetTypeCall=true  

### docker 생성하기
https://hub.docker.com/ --> registry 등록  

### 리눅스에 도커 설치하기
- script로 설치 (루트권한 요구됨)  
$ curl -fsSL https://get.docker.com/ | sudo sh  
또는 $ sudo wget -qO- http://get.docker.com/ | sh  
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

- 버전확인 했을 시, **Error: got permission denied while trying to connect to the docker daemon socket** 해결은  
$ sudo chmod 666 /var/run/docker.sock 실행하기  
(참고: https://github.com/palantir/gradle-docker/issues/188 )
![image](https://user-images.githubusercontent.com/56099627/89254188-8af58100-d659-11ea-9b6b-4d959ea29681.png)  

- 문제발생, **Error loading config file: /home/$USER/.docker/config.json: open /home/$USER/.docker/config.json: permission denied**  
해결: https://askubuntu.com/questions/747778/docker-warning-config-json-permission-denied   
터미널에서 echo $USER 으로 $USER 확인해 볼것!  
$ sudo chown "$USER":"$USER" /home/"$USER"/.docker -R  
$ sudo chmod g+rwx "/home/$USER/.docker" -R  
문제발생 캡쳐:  
![image](https://user-images.githubusercontent.com/56099627/129864427-ab95431c-1a85-4687-8dff-ccab69da799a.png)  
문제해결 캡쳐:  
![image](https://user-images.githubusercontent.com/56099627/129864677-0c597902-a2a1-4577-83e9-6b9e513504e2.png)  



### nvidia docker 설치
http://blog.naver.com/PostView.nhn?blogId=doksg&logNo=221467903478&parentCategoryNo=&categoryNo=19&viewDate=&isShowPopularPosts=false&from=postView   
- nvidia-docker는 nvidia gpu를 사용할수 있도록 해주는 docker로 다른 CUDA version을 사용할수 있도록 해준다. 
```
$ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
$ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
$ sudo apt-get update
```
![image](https://user-images.githubusercontent.com/56099627/98925396-46f7ff00-2519-11eb-937f-d12708b7b304.png)  
- 위에 내용을 복붙해서 넣으면 sudo apt-get으로 nvidia-docker2를 설치할수 있도록 repo가 추가된다.  
$ sudo apt-get install nvidia-docker2  
![image](https://user-images.githubusercontent.com/56099627/98925635-92aaa880-2519-11eb-894f-adf8ff4f3a8d.png)  

### docker hub 이미지 레파지토리에 올리고 삭제하기
1. 레파지토리 로그인 하기  
![image](https://user-images.githubusercontent.com/56099627/89258912-1a079680-d664-11ea-95ee-2e2cac7a6466.png)  
2. 도커 이미지 commit 하여 새로운 도커 이미지 만들기  
$ docker commit <container ID> <만들고자 할 이미지 이름>:<만들고자하는 Tag>  
![image](https://user-images.githubusercontent.com/56099627/97673340-f7541500-1ace-11eb-9576-8d61da78771e.png)  
![image](https://user-images.githubusercontent.com/56099627/94108972-37462d80-fe7b-11ea-87ae-98f4821d23bc.png)
**만약에 도커 허브에 이미지 올리기 위해선 Repasitory 이름과 dockerhub ID/이미지 이름 이 일치해야 한다!**  
**Repasitory 이름, dockerhub ID/이미지 이름 불일치 한다면, "denied: requested access to the resource is denied " 라는 메세지와 함께 도커 허브에 이미지가 올라가지 않는다**  
실패 예시  
![image](https://user-images.githubusercontent.com/56099627/94109850-922c5480-fe7c-11ea-976e-90da9b363797.png)  
성공 예시  
![image](https://user-images.githubusercontent.com/56099627/94110070-fa7b3600-fe7c-11ea-83f1-f9443ce496db.png)  
2-2. (선택) 로컬 이미지에 태그 설정  
$ docker tag <업로드할 이미지의 ID> <이미지 이름>:<새로운 태그이름>   
![image](https://user-images.githubusercontent.com/56099627/94109153-868c5e00-fe7b-11ea-9c40-61830cc1839e.png)  
3. 이미지 올리기  
$ docker push <docker hub ID>/<>
$ docker push hihijimin/dockerlab:base  
![image](https://user-images.githubusercontent.com/56099627/89259251-dbbea700-d664-11ea-9e84-1aab87a9af62.png)  

### **종료된 contatiner에 다시 접속하기**
```
1. $ docker ps -a 으로 컨테이너가 있는지 확인한다
2. $ docker start [container_ID] 
3. $ docker ps 으로 컨테이너가 실행 되었는지 확인한다
4. $ docker exec -it [contatiner_ID] /bin/bash
```

### container 강제?종료 시키기
$ docker kill [containner ID]   → 현재 실행중인 모든 컨테이너 강제 종료  
$ docker stop [containner ID]   → 현재 실행중인 모든 컨테이너 종료  
![image](https://user-images.githubusercontent.com/56099627/93839538-34efa200-fcc8-11ea-94f3-e01a829f807a.png)
  
### docker 실행 & nvidia-docker 개발환경 셋팅
https://hiseon.me/linux/ubuntu/install-docker/  
https://hub.docker.com/r/nvidia/cuda/tags/  
https://jybaek.tistory.com/791  
```
--rm: 프로세스 종료시 컨테이너 자동 제거, -it: -i와 -t을 동시에 사용한것임 터미널 입력을 위한 옵션(컨테이너의 표준 입력과 로컬 컴퓨터의 키보드 입력을 연결)
```
- 도커에 nvidia toolkit 10.2 설치  
1. https://hub.docker.com/r/nvidia/cuda/tags/ 에 들어가서 원하는 버전 선택하여 컨테이너 이미지 다운로드 하기
2. 아래의 명령어는 CUDA Toolkit 10.2 버전의 컨테이너 이미지를 다운 받고($ docker pull nvidia/cuda:10.2-base), nvidia-smi 명령어를 실행
/bin/bash 명령어를 실행한 예제  
$ docker run -it nvidia/cuda:10.2-base /bin/bash  
container_name, port 정보 포함한 /bin/bash 명령어를 실행한 예제  
$ docker run -it --gpus all --name simple_pose -p 8888:8888 nvidia/cuda:10.2-base /bin/bash  
![image](https://user-images.githubusercontent.com/56099627/90747520-fc952680-e30b-11ea-9727-524f7af68418.png)  
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
3. ananconda 설치(선택)  
$ wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh  
$ bash Anaconda3-2020.07-Linux-x86_64.sh  
![image](https://user-images.githubusercontent.com/56099627/90592994-e14dec80-e221-11ea-8ebf-6992ceadb8d5.png)  
4. pip & python 설치
$ apt install python-pip  
$ apt install python3-pip  
5. jupyter notebook 설치 & 실행  
$ pip3 install notebook  
$ jupyter notebook --ip=0.0.0.0 -port=8888 --allow-root  
![image](https://user-images.githubusercontent.com/56099627/90755199-dd9b9200-e315-11ea-91fe-a1614a07c299.png)  
**아래와 같이 docker 오픈할 때 --ip 와 -port 가 jupyter notebook 실행시 일치해야 함**  
![image](https://user-images.githubusercontent.com/56099627/91705759-5de4b180-ebb8-11ea-93e5-8386dcb999c9.png)  
![image](https://user-images.githubusercontent.com/56099627/91705802-6e952780-ebb8-11ea-84b7-a3ed8b7925d8.png)  
- **패키지 설치시 에러 발생**  
(업데이트 안해줘서 생긴듯?) 해결 방법: $ **apt update**  
<에러발생 예시>  
![image](https://user-images.githubusercontent.com/56099627/93560537-5ba69380-f9bd-11ea-87c3-afa429ffe76b.png)  
<결과 예시>  
![image](https://user-images.githubusercontent.com/56099627/93560750-ce177380-f9bd-11ea-90c1-6fcc71a7a373.png)  

### docker option 
http://pyrasis.com/book/DockerForTheReallyImpatient/Chapter20/28  

### docker local-docker 파일올리기
참고: https://itholic.github.io/docker-copy/  
1. 로컬파일을 도커에 복사(특정 경로)  
$ dockr cp 경로/file.txt [container ID]:경로  
예) $ docker cp ~/data/test.md tmp_container:/root/data  
![image](https://user-images.githubusercontent.com/56099627/97387413-45271c80-1919-11eb-9e4e-0fcbe444689c.png)  
2. 도커파일을 로컬에 복사(특정 경로)  
$ dockr cp [container ID]:경로/file.txt 경로  
예) $ docker cp tmp_container:/root/data/test.md ~/data/  

### docker 저장위치 변경
https://yookeun.github.io/docker/2018/10/29/docker-change/  
http://dveamer.github.io/backend/DockerImageDirectory.html  
https://hooni-playground.com/2019/12/05/docker-%EC%A0%80%EC%9E%A5%EC%86%8C-%EC%9C%84%EC%B9%98-%EB%B3%80%EA%B2%BD/ 
1. 위치 변경 전 확인(꼭 sudo로 해야함)  
$ sudo lsof | grep /var/lib/docker  
'/var/lib/docker' 디렉토리에 위치한 여러파일들을 dockerd, docker-co 프로세스들이 사용중인 것을 확인할 수 있음  
![image](https://user-images.githubusercontent.com/56099627/90712640-731b2f80-e2de-11ea-8d74-336d43aecb33.png)  
2. docker 실행 서비스에서 설정변경 & Docker 프로세스 중지  
/lib/systemd/system/docker.service 파일을 열고 아래 내용을 수정한다.  
#ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock  
#ExecStart=/usr/bin/dockerd -g /New_dir/docker -H fd:// --containerd=/run/containerd/containerd.sock  
ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock --data-root=/data/  
수정이 되면 도커를 중지시킨다.  
$ sudo systemctl stop docker  
$ sudo systemctl daemon-reload  
![image](https://user-images.githubusercontent.com/56099627/90723669-293f4300-e2f8-11ea-8c16-ea2c6bc7b225.png)  
3. Docker NEW 저장 경로 만들기 & NEW 경로로 Docker 복제  
도커 데이터가 저장될 경로를 먼저 만들어주어야 한다.  
$ mkdir /home/ykkim/docker  
그런 다음 기존에 docker 경로를 위 경로로 통째로 복제해준다.  
$ sudo rsync -aqxP /var/lib/docker /home/ykkim/docker  
3-1. 도커 설정 파일을 만든다  
$ sudo vim /etc/docker/daemon.json  
```
{
    "data-root": "/storage/repository/docker"
}
```
4. 마지막 이제 도커를 실행  
$ sudo systemctl start docker  
5. 잘 옮겨졌는지 확인
$ ps -ef | grep docker  
$ docker info | grep Root  
![image](https://user-images.githubusercontent.com/56099627/90994606-3d36bd80-e5f4-11ea-9345-9ceed2802ef6.png)  

### docker 설치하고 첫번째 run 할때 발생 에러
**issue: docker: Error response from daemon: could not select device driver "" with capabilities: [[gpu]].
ERRO[0000] error waiting for container: context canceled**  
https://github.com/NVIDIA/nvidia-docker/issues/1034  
- 해결방안: **$ sudo systemctl restart docker**  
- 에러 & 해결 인증  
![image](https://user-images.githubusercontent.com/56099627/98921012-26797600-2514-11eb-9998-0004a1ddbce3.png)  
![image](https://user-images.githubusercontent.com/56099627/98921390-9687fc00-2514-11eb-86d2-468c3f7864c8.png)  
**issue: docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.40/containers/create: dial unix /var/run/docker.sock: connect: permission denied.**  

### docker에 화면 공유
· (먼저)$ xhost +local:docker  
※ 호스트에서 토커가 Xserver와 통신할 수 있도록 설정함  
· (또는)$ xhost +local:root    
![image](https://user-images.githubusercontent.com/56099627/131605767-7a4f9a56-73d1-4768-8bf6-a527b27ac9f6.png)  
[error 해결 링크](https://eungbean.github.io/2018/12/04/EOD-cannot-connect-to-X-server-0.0/)  
```  
문제상황: docker에서 opencv를 사용하려고 했는데, 이미지를 띄우는 과정에서 오류 남
error message :  
No protocol specified
: cannot connect to X server :1  

해결방안: local 터미널에서 $ xhost +local:root 명령 실행해준다
```

· $ docker run … -v /tmp/.X11-unix:/tmp/.X11-unix:ro -e DISPLAY=$DISPLAY  
※ 호스트의 XServer를 볼륨 형태로 공유 (ro : Readonly), DISPLAY 환경변수 전달  
※ XSever소켓은 ‘/tmp/.X11-unux’에 존재한다.  

· 예시
$ docker run --gpus all -it --privileged --ipc=host -v /home/jimin/HDD1/AiPose:/workspace -w /workspace -p 8080:8080 --name iter_pose_trt -v /home/jimin/HDD2/DB:/workspace/DB -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY hict/aipose:20210305

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
