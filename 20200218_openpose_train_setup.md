참고 1  
https://tobeagoodmom.tistory.com/2174  
- 1. 가상환경 만들어주고 (파이썬 환경 셋업)
  - 명령어 **(base) C:\Users\humanict>conda create --name caffe_dev**
  - 가상환경 활성화 **(base) C:\Users\humanict>conda activate caffe_dev**
- 2. opencv 셋업  
  - **(caffe_dev) C:\Users\humanict>conda install opencv=4.2.0**
- 3. 라이브러리 셋업
  - **(caffe_dev) C:\Users\humanict>conda install scikit-image**  
- 4. CUDA 설치 되어 있다면 패스
- 5. caffe 셋업
# caffe 셋업
- 참고1: 설치하는 방법 매우 자세히 잘 나와있음!!
https://baemincheon.tistory.com/21  
- 참고2: 에러에 대처하는 방법 자세히 나와 있음(중국어)!!
https://www.geek-share.com/detail/2748721992.html  
  
![image](https://user-images.githubusercontent.com/56099627/74830132-cde6c500-5355-11ea-9ecf-cd6e4c29a617.png)  
  
![image](https://user-images.githubusercontent.com/56099627/74830178-ea82fd00-5355-11ea-84f1-143d0bc5dfb3.png)  

![image](https://user-images.githubusercontent.com/56099627/74891412-5010d100-53ca-11ea-8c54-2806b53d4021.png)  
  
- 이부분을 변경했음 그 결과
D:\caffe\cmake\WindowsDownloadPrebuiltDependencies.cmake 에서  
이전(f060403fd1a7448d866d27c0e5b7dced39c0a607) -> 변경(d04c905437d24bf5fe629829ecbebb94713c6724)  

    set(DEPENDENCIES_URL_1900_35 "${DEPENDENCIES_URL_BASE}/v${DEPENDENCIES_VERSION}/${DEPENDENCIES_NAME_1900_35}${DEPENDENCIES_FILE_EXT}")
    set(DEPENDENCIES_SHA_1900_35 "d04c905437d24bf5fe629829ecbebb94713c6724")
  
![image](https://user-images.githubusercontent.com/56099627/74897614-fc5ab380-53da-11ea-9869-8cd837fadcb3.png)  
![image](https://user-images.githubusercontent.com/56099627/74897659-1a281880-53db-11ea-81f9-f6ed2f7fdd6a.png)  
![image](https://user-images.githubusercontent.com/56099627/74897720-43e13f80-53db-11ea-9706-cc2bb5b32904.png)  
![image](https://user-images.githubusercontent.com/56099627/74897751-607d7780-53db-11ea-9e2b-a6aaddd640b8.png)  





git clone https://github.com/BVLC/caffe.git  
cd caffe  
cp Makefile.config.example Makefile.config (해당 폴더-파일 들어가서 수정하기!)  

    < 아나콘다 파이썬을 사용한다면 이 부분 찾아 **주석 처리** 하기 >
    Makefile.config 파일에서 두가지만 체크!
    CPU_ONLY := 1
    PYTHON_INCLUDE := /usr/local/include/python2.7 \
                                              /usr/local/include/python2.7/numpy

    < 아나콘다 파이썬을 사용한다면 이 부분 찾아 **주석 해제** 하기 >
    ANACONDA_HOME := $(HOME)/anaconda 
    PYTHON_INCLUDE := $(ANACONDA_HOME)/include \ 
      # $(ANACONDA_HOME)/include/python2.7 \ 
      $(ANACONDA_HOME)/lib/python2.7/dist-packages/numpy/core/include \

    # We need to be able to find libpythonX.X.so or .dylib. 
    # PYTHON_LIB := /usr/lib PYTHON_LIB := $(ANACONDA_HOME)/lib

# OpenBLAS 셋업
참고 2  
https://seonho.gitbooks.io/deep-learning-with-python/chap1/native/OpenBLAS.html  
![image](https://user-images.githubusercontent.com/56099627/74723655-4da16080-527e-11ea-8f7c-bd4bdfec5602.png)  

# boost 셋업
D:/openpose_caffe_train-master  
D:/openpose_caffe_train-master/build  
이렇게 빌드 시키려고 하니 아래 그림과 같이 오류가 떴다.  
보니, boost을 설치하랜다  
![image](https://user-images.githubusercontent.com/56099627/74799580-488ef080-5314-11ea-9603-284f66abfb21.png)
- 참고 1: https://wendys.tistory.com/115
- 참고 2: https://redcoder.tistory.com/143
- step 1) boost 다운로드
  - boost 다운로드 받는 공식 사이트 : https://www.boost.org/users/download/
- step 2) 다운로드 받은 것을 압축 해제 한다음 (경로 결과: D:\boost_1_72_0 ) **boostrap.bat 실행 하면 b2.exe, cjam.exe 파일 생성됨**
  - 나의 경우엔 b2.exe, cjam.exe 파일이 ./ 경로에 바로 생성되지 않아서 검색해보니 ./../engine/ 경로에 이 두개 파일이 생성되어서 이것을 ./ 복사해서 경로 밖으로 빼어 주었음(빼준 이유는 다음 step 실행하기 위해서) 
- step 3) 명령 프롬프트 **C:\Program Files (x86)\boost\boost_1_72_0>** 으로 들어간다. 그런후 아래 명령어를 실행하면 빌드 된다. 
  - 명령 프롬프트에서 명령어: **b2 --toolset=msvc-14.0 variant=debug,release address-model=64 threading=single,multi runtime-link=static,shared**
  - 32bit (x86) 빌드(vs2015) 쓰는 사람은 --toolset=msvc-14.0, address-model=32 이렇게 작성
  - 64bit (x86) 빌드(vs2015) 쓰는 사람은 --toolset=msvc-14.0, address-model=64 이렇게 작성 
- 참고! 참고 2 에서 알려준 방법인데 boost을 직접 빌드 하기 시르면 https://sourceforge.net/projects/boost/files/boost-binaries/ 으로 가서 빌드된 것을 다운로드 받으랜다.

두번째 에러
https://sourceforge.net/projects/boost/files/boost-binaries/ 에서 **boost_1_71_0-msvc-14.0-64.exe**을 다운로드 받은 후,  
C:/local/boost_1_17_0 경로로 설치 하였더니 아래 그림과 같은 에러 메세지 뜸  
![image](https://user-images.githubusercontent.com/56099627/74816686-f3b49f80-533e-11ea-9da1-e06bb741867d.png)  

- windows powershell 관리자 권한으로 들어가서 choco 을 설치함
  - 명령어: PS C:\Windows\system32> **Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))**
  - choco 버전 확인 : 명령어 **choco -v**, sudo 설치 명령어 : **choco install sudo**  
  
![image](https://user-images.githubusercontent.com/56099627/74817181-d6cc9c00-533f-11ea-899c-310e00c9ef4c.png)  
