## 환경 셋팅
1. https://github.com/stefanopini/simple-HRNet 에서 직접 다운로드함 적절한 경로에 둠  
2. 위 경로에 pycharm 새 프로젝트 열기  
3. 패키지 설치(최소한 설치)  
requirements.txt list

    ffmpeg-python>=0.2.0
    matplotlib>=3.0.2
    munkres>=1.1.2
    numpy>=1.16
    opencv-python>=3.4
    Pillow>=5.4
    vidgear>=0.1.4
    torch>=1.4.0
    torchvision>=0.5.0
    tqdm>=4.26
    tensorboard>=1.11
    tensorboardX>=1.4

1) opencv 설치  
: numpy, opencv-contrib-python 함께 설치됨  

$ pip install opencv-contrib-python  
(numpy 패키지 까지 같이 설치됨)  
: (requirements) numpy>=1.16, opencv-python>=3.4  
![image](https://user-images.githubusercontent.com/56099627/82406846-9d244200-9aa2-11ea-8d1f-554deb6b0117.png)  
$ pip install opencv-python  
![image](https://user-images.githubusercontent.com/56099627/82530832-227a2600-9b79-11ea-8ff4-0f7e97c1d2cd.png)  

2) torch 설치  
: torch, torchvusion, future, pillow 함께 설치됨  
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

3) ffmpeg-python (0.2.0)  
$ pip install ffmpeg-python  
![image](https://user-images.githubusercontent.com/56099627/82528953-e2b13f80-9b74-11ea-8215-342d59e5d612.png)  

4) matplotlib (3.2.1)  
: six, python-dateutil, pyparsing, kiwisolver, cycler, matplotlib 함께 설치됨  
$ pip install matplotlib  
![image](https://user-images.githubusercontent.com/56099627/82529048-15f3ce80-9b75-11ea-9359-6e5bd7c1e5ea.png)  

5) munkres (1.1.2)  
$ pip install munkres  
![image](https://user-images.githubusercontent.com/56099627/82529196-666b2c00-9b75-11ea-8186-7e459662eca4.png)  

6) vidgear==0.1.4  
: idna, chardet, urllib3, requests, pafy, youtube-dl, vidgear 함께 설치됨  
$ pip install vidgear==0.1.4  
![image](https://user-images.githubusercontent.com/56099627/82529379-d8437580-9b75-11ea-80b1-f9eaff930b8a.png)  

7) tqdm (4.46.0)  
$ pip install tqdm  
![image](https://user-images.githubusercontent.com/56099627/82529513-26587900-9b76-11ea-8444-5dde1f6f7212.png)  

8) tensorboard (2.2.1)  
: absl-py-0.9.0 cachetools-4.1.0 google-auth-1.15.0 google-auth-oauthlib-0.4.1 grpcio-1.29.0 importlib-metadat a-1.6.0 markdown-3.2.2 oauthlib-3.1.0 protobuf-3.12.1 pyasn1-0.4.8 pyasn1-modules-0.2.8 requests-oauthlib-1.3.0 rsa-4.0 tensorboard-2.2.1 tensorboard-plugin-wit-1.6.0.post3 werkzeug-1.0.1 zipp-3.1.0 함께 설치  
$ pip install tensorboard  
![image](https://user-images.githubusercontent.com/56099627/82529862-e940b680-9b76-11ea-863c-4950e4500302.png)  
![image](https://user-images.githubusercontent.com/56099627/82529922-07a6b200-9b77-11ea-9882-d1310aca099f.png)  

9) tensorboardX (2.0)  
$ pip install tensorboardX  
![image](https://user-images.githubusercontent.com/56099627/82530601-a41d8400-9b78-11ea-98d8-0d680f6434e4.png)  

