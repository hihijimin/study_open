https://webnautes.tistory.com/1413  
### 셋업 
1. qt 설치 파일 다운로드  
공식 사이트(http://download.qt.io/archive/qt/)에 들어가 리눅스용 설치파일(qt-opensource-linux-x64-5.14.2.run) 다운로드  

2. 필수 파일 설치 및 업데이트
- 패키지 리스트 업데이트: $ sudo apt-get update
- build-essential 패키지(C/C++ 컴파일러와 C/C++를 위한 라이브러리, 헤더파일, make같은 유틸리티 도구 등이 포함): $ sudo apt-get install build-essential  
![image](https://user-images.githubusercontent.com/56099627/98632328-a829a200-2362-11eb-8453-18887a8f41fc.png)  
- Qt4 있다면 제거 : $ sudo apt-get purge --auto-remove libqt4-dev  
![image](https://user-images.githubusercontent.com/56099627/98632377-c1325300-2362-11eb-9af2-393d7ee7c48d.png)  

3. 설치 진행 
- 다운로드 받은 디렉토리에서 chmod 명령으로 퍼미션 변경 후, 설치 실행  
$ chmod +x qt-opensource-linux-x64-5.14.2.run  
$ ./qt-opensource-linux-x64-5.14.2.run  
- Qt ui 생성되면, 로그인 하고 설치 진행 ~

- 환경변수 수정




