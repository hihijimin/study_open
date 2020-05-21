## 환경 셋팅
1. https://github.com/stefanopini/simple-HRNet 에서 직접 다운로드함 적절한 경로에 둠  
2. 위 경로에 pycharm 새 프로젝트 열기  
3. 패키지 설치(최소한 설치)  
1) opencv 설치  
$ pip install opencv-contrib-python  
(numpy 패키지 까지 같이 설치됨)  
: (requirements) numpy>=1.16, opencv-python>=3.4  
![image](https://user-images.githubusercontent.com/56099627/82406846-9d244200-9aa2-11ea-8d1f-554deb6b0117.png)  
2) torch 설치  
: (requirements) torch>=1.4.0, torchvision>=0.5.0  
참고사이트 https://pytorch.org/  
conda 설치  
$ conda install pytorch torchvision cudatoolkit=9.0 -c pytorch -c defaults -c numba/label/dev  
이건 torch 1.1.0 버전 설치므로 안됌!!
![image](https://user-images.githubusercontent.com/56099627/82408649-027a3200-9aa7-11ea-88e7-f60da4bf9cae.png)  
$ conda install pytorch torchvision cudatoolkit=10.0 -c pytorch -c defaults -c numba/label/dev  
이건 torch 1.2.0 버전 설치므로 안됌!!
![image](https://user-images.githubusercontent.com/56099627/82410108-2db25080-9aaa-11ea-99a6-102bb99ed651.png)    

==> cuda 9.2으로 재설치 한 후, pip으로 torch 설치  
![image](https://user-images.githubusercontent.com/56099627/82527503-96183500-9b71-11ea-8f23-459fb8c69ee6.png)  
pip 설치
$ pip install torch==1.5.0+cu92 torchvision==0.6.0+cu92 -f https://download.pytorch.org/whl/torch_stable.html
![image](https://user-images.githubusercontent.com/56099627/82527467-800a7480-9b71-11ea-9d34-34cc4bb9e58f.png)  


