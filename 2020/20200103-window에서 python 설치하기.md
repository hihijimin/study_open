# 아나콘다로 파이썬 설치
나중에~  

# pip으로 파이썬 모듈 설치
- 현재 내꺼 PC에 파이썬 3.7버전 설치 되었음
![image](https://user-images.githubusercontent.com/56099627/71706649-96659d00-2e29-11ea-818d-368618d7ed36.png)  
- 프롬프트에서 python 들어가기 (잘 들어가지지?)
![image](https://user-images.githubusercontent.com/56099627/71706701-f1978f80-2e29-11ea-90f4-13c6a9c4c171.png) 
- pip 으로 opencv 모듈 설치하기 
![image](https://user-images.githubusercontent.com/56099627/71706815-46d3a100-2e2a-11ea-90cf-9c01bd3930ef.png)  
- 해당 경로에 환경 변수 설정해주기

# anaconda navigator 으로 가상환경 생성
![image](https://user-images.githubusercontent.com/56099627/71880789-69402400-3174-11ea-93a8-422a02cf5551.png)
- base(root) 옆 삼각형을 누르면 <open Terminal> 실행하면 검정 프롬프트 화면이 나옴
- 'conda update conda' 라고 작성한다. 
![image](https://user-images.githubusercontent.com/56099627/71881281-5e39c380-3175-11ea-8fe0-1851ca156388.png)
- conda createe -n 가상환경 이름 : <가상환경 이름>의 이름으로 가상환경을 생성한다.
  - ex) conda create -n text : text 란 이름의 가상환경 생성
![image](https://user-images.githubusercontent.com/56099627/71881463-afe24e00-3175-11ea-90d1-2a9df5a4e56f.png)  
- 그런 후, 가상환경이 올바르게 생성됐는지 확인 해 보기 위해서 'conda info --envs'라고 작성하여 가상환경 목록을 조회한다.
- 올바르게 생성된 것을 확인 할 수 있음
![image](https://user-images.githubusercontent.com/56099627/71881680-16676c00-3176-11ea-86fa-97e697cdfd74.png)  
- 생성된 가상환경이 활성화 시키기 : **activate <가상환경 이름>** 작성
  - 가상환경을 비활성화 방법: deacticate 작성

# cudnn 설치하기
![image](https://user-images.githubusercontent.com/56099627/71951429-5f72fb00-321e-11ea-9b1d-55650ce01e3e.png)
- cuda 10.2 다운로드 하기 
  -링크: https://developer.nvidia.com/cuda-downloads
- cuda 10.2 **빠른 설치**로 진행
![image](https://user-images.githubusercontent.com/56099627/71951523-aeb92b80-321e-11ea-9343-5b2b0227db42.png)
  
- cuDnn 설치 for cuda 10.2
  - 링크: https://developer.nvidia.com/rdp/cudnn-download (로그인 후 다운로드 가능)
![image](https://user-images.githubusercontent.com/56099627/71951869-e379b280-321f-11ea-88d5-09d4394e2314.png)
- cuDnn 파일을 다운로드 받으면 zip 파일로 되어 있음 압축을 풀면 3개의 폴더가 보임
- cuda을 설치했다면 아래 경로에 쿠다 있음
  - **C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.2**
  ![image](https://user-images.githubusercontent.com/56099627/71952116-df9a6000-3220-11ea-97ef-4f77e80d3d5f.png)
  - 압축을 푼 3개의 폴더의 내용을 해당 경로에 **덮어씌어 준다**. (bin, include, lib 폴더에는 각각 cudnn의 dll, lib, 헤더 파일이 생겼을 것임)

# 가상환경 
## 1. 가상환경 생성
- **conda create -n 가상환경이름 python=3.6 ** 작성
## 2. 가상환경 Activation
- **activate 가상환경이름** 작성
## 3. TensorFlow GPU 설치
- **conda install -c anaconda tensorflow-gpu **  작성
## 3-1. TensorFlow GPU 버전 설정하여 설치 시 
- conda install -c anaconda tensorflow-gpu=1.x
- conda install -c anaconda cudnn=7.x.x or ... 
- conda install -c anaconda cudatoolkit=9.x or 10.x ... 
- (필요시) conda install -c menpo opencv
- 원하는 버전 tensorflow 설치 명령어: pip install --ignore-installed --upgrade tensorflow==1.4.0  
![image](https://user-images.githubusercontent.com/56099627/75418128-0732bc80-5976-11ea-8f15-973773e846a0.png)  

# 가상환경에 Tensorflow 설치하기 
- 참고로 cmd을 이용해 모듈을 설치할 때는 pip을 사용한다. 하지만 아나콘다에서는 conda을 사용하는 것이 좋다
  
- **conda install tensorflow** 작성한다: tensorflow 설치하기  
  - proceed(y/n)? 나오면 y
  - 설치 할 때 인터넷 접속이 원활해야함  
![image](https://user-images.githubusercontent.com/56099627/71882178-4ebb7a00-3177-11ea-91af-d514711d2adb.png)  
- 올바른게 tensorflow 설치 됐는지 확인해 보기 위해 **conda list**을 작성하여 가상환경에 설치된 패키지와 모듈을 조회한다
  - 참고로 설치되고 나면 38개의 패키지가 설치 된다.  
![image](https://user-images.githubusercontent.com/56099627/71882305-8f1af800-3177-11ea-8900-f7a6f9466d41.png)
- 완료된 tensorflow 결과 화면

### YOLO-v3 실행하기 위해선 tensorflow 1.12 버전이 있어야함
- tensorflow 1.12 버전 설치 전, anaconda3-5.2.0-windows-x86_64.exe을 설치한다(파이썬 3.6) 아래 링크로 다운로드!
  -링크: https://repo.anaconda.com/archive/Anaconda3-5.2.0-Windows-x86_64.exe
![image](https://user-images.githubusercontent.com/56099627/71955306-43c22180-322b-11ea-90b5-597f81a72702.png)
-원하는 tensorflow 버전(1.12.0) 설치방법 : **pip install tensorflow-gpu==1.12.0** 작성한다
- import 했을 때 문제가 없는지 확인한다
  - import tensorflow as tf , print(tf.__version__)

# 가상환경에 jupyter, spyder 설치 하기
- 일반적으로 바로 jupyter, spyder 실행하면 무조건 root 계정의 가상환경으로 바탕으로 작동하기 때문에  가상환경이 활성화된 상태에서 다음과 같이 입력해야 함
  - **conda install jupyter notebook** : jupyter notebook 설치
  - **jupyter notebook** : jupyter notebook 실행
  - **conda install spyder** : spyder 설치
  - **spyder** : spyder 실행

# 가상환경에 opencv 패키지 설치하기
![image](https://user-images.githubusercontent.com/56099627/71884104-03a36600-317b-11ea-8bbf-12a94aba3cb9.png)
- **pip install opencv-contrib-python** 작성

# Anaconda PIL(python image library) 설치하기
![image](https://user-images.githubusercontent.com/56099627/71964489-049ecb00-3241-11ea-9ee6-12efaf1b7754.png)
- **conda install pillow**
![image](https://user-images.githubusercontent.com/56099627/71885166-26367e80-317d-11ea-9cf0-548d70c6e843.png)
- < from PIL import Image > 이렇게쓰는 패키지 설치하기 위해 **pip install <설치경로>\<해당하는 pil 파일 다운로드 받고 그 다운로드받은 이름>** 
  - **pip install C:\Pillow-7.0.0-cp37-cp37m-win_amd64.whl** 라고 작성하기

# windows 가상환경에 wget 설치하기
- 먼저, **wget.exe**을 다운로드 한다 (참고 [3]링크 들어가서 받기)
- 다운로드 받은 wget.exe 파일을 **C:\Windows\System32 폴더**에 넣어준다
![image](https://user-images.githubusercontent.com/56099627/71944747-1d3ebf00-3208-11ea-8226-884333b0bfa5.png)  
- 그런 후, wget을 실행해본다 (예제로 구글 이미지 로고 다운로드 받는거 해봄 : 잘 실행 되는 것을 확인함)

참고  
[1] https://nomis.tistory.com/115,  [Python] 설치 & pip 이용 방법  
[2] https://pythonkim.tistory.com/137, 윈도우10 + 텐서플로 GPU 버전 설치
[3] https://gameseven.tistory.com/538, 아나콘다로 텐서플로우 설치방법  
[4] https://zvi975.tistory.com/65, Anaconda에 Tensorflow 설치, 사용하기  
[5] https://synchronized.tistory.com/entry/wget%EC%9D%84-%EC%9C%88%EB%8F%84%EC%9A%B0%EC%97%90%EC%84%9C-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EC%9E%90, wget을 윈도우에서 사용해보자!!  
[6] https://eehoeskrap.tistory.com/293, [TensorFlow] Anaconda 가상환경 이용하여 TensorFlow GPU 설치  
