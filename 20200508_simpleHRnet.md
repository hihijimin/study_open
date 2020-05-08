## simple HRnet 설치
빠른 video_demo을 위해~~ 설치.  
HRnet2019버전으로 pose estimation 한 것임  
https://github.com/stefanopini/simple-HRNet  
  
1. 설치 시작  
1-1. $ pip install -r requirements.txt 실행
![image](https://user-images.githubusercontent.com/56099627/81363128-8c2c1600-911d-11ea-90f1-c6fe01cf569e.png)  
![image](https://user-images.githubusercontent.com/56099627/81365837-2ee79300-9124-11ea-8130-b41e0bb62815.png)  
![image](https://user-images.githubusercontent.com/56099627/81365914-648c7c00-9124-11ea-94c1-cae84ecbbeed.png)  
"ERROR: bravado 10.6.0 requires simplejson, which is not installed." 에러로 인해 bravado 만 추가로 따로 설치  
![image](https://user-images.githubusercontent.com/56099627/81363488-68b59b00-911e-11ea-8d6a-c4919c55b93f.png)  
요구하는 requirment가 다 설치 되었느지 확인 차원에서 다시 "$ pip install -r requirements.txt" 실행해봄 --> 이미 다 설치된 파일 이라 나옴
1-2. support 으로서 yolo 설치
https://github.com/eriklindernoren/PyTorch-YOLOv3/tree/47b7c912877ca69db35b8af3a38d6522681b3bb3
Install YOLOv3 required packages으로서 requirements.txt을 설치해야 하는데   
$ pip install -r requirements.txt (from folder ./models/detectors/yolo)  
numpy  
torch>=1.0  
torchvision  
matplotlib  
tensorflow <-----요거 두개가 섬뜩함~ 버전을 바꿔야 해서  
tensorboard <----  
terminaltables  
pillow  
tqdm  
아니나 다를까 이런 에러가 뜸  
"ERROR: tensorflow-gpu 1.14.0 has requirement tensorflow-estimator<1.15.0rc0,>=1.14.0rc0, but you'll have tensorflow-estimator 2.2.0 which is incompatible.  
ERROR: tensorflow 2.2.0 has requirement tensorboard<2.3.0,>=2.2.0, but you'll have tensorboard 1.14.0 which is incompatible.  
Installing collected packages: astunparse, tensorflow-estimator, tensorflow, terminaltables  
  Attempting uninstall: tensorflow-estimator  
    Found existing installation: tensorflow-estimator 1.14.0  
    Uninstalling tensorflow-estimator-1.14.0:  
ERROR: Could not install packages due to an EnvironmentError: [Errno 13] 허가 거부: 'METADATA'  
Consider using the `--user` option or check the permissions.  "
![image](https://user-images.githubusercontent.com/56099627/81364528-d236a900-9120-11ea-8d08-a8942809f0fc.png)  
![image](https://user-images.githubusercontent.com/56099627/81364564-ee3a4a80-9120-11ea-814c-8d064187c98d.png)  
