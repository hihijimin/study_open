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
![image](https://user-images.githubusercontent.com/56099627/71885166-26367e80-317d-11ea-9cf0-548d70c6e843.png)
- < from PIL import Image > 이렇게쓰는 패키지 설치하기 위해 **pip install <설치경로>\<해당하는 pil 파일 다운로드 받고 그 다운로드받은 이름>** 
  - **pip install C:\Pillow-7.0.0-cp37-cp37m-win_amd64.whl** 라고 작성하기

참고  
[1] https://nomis.tistory.com/115,  [Python] 설치 & pip 이용 방법  
[2] https://zvi975.tistory.com/65, Anaconda에 Tensorflow 설치, 사용하기
