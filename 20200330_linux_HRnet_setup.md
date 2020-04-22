https://github.com/HRNet 
L HRNet-Image-Classification  
L HRNet-Object-Detection  
L HRNet-Semantic-Segmentation  
L HigherHRNet-Human-Pose-Estimation  
L HRNet-Human-Pose-Estimation  
L HRNet-Facial-Landmark-Detection  

## HigherHRNet-Human-Pose-Estimation  
https://github.com/HRNet/HigherHRNet-Human-Pose-Estimation  

the latest version pytorch  
conda install pytorch torchvision cudatoolkit=10.0  
![image](https://user-images.githubusercontent.com/56099627/78003556-ce6e7480-7373-11ea-9ddd-581c63e53585.png)  

## HRNet-Object-Detection  
https://github.com/HRNet/HRNet-Object-Detection  

This code is developed using on **Python 3.6 and PyTorch 1.0.0** on Ubuntu 16.04 with NVIDIA GPUs.  
https://pytorch.org/get-started/previous-versions/  
command: conda install pytorch==1.0.0 torchvision==0.2.1 cuda100 -c pytorch  
![image](https://user-images.githubusercontent.com/56099627/78114996-19a08a00-743d-11ea-985f-ea6a45b98456.png)  

code download  
HRNet-Object-Detection folder  
L Install pycocotools  
  ![image](https://user-images.githubusercontent.com/56099627/78117523-bc0e3c80-7440-11ea-9813-8c28b08e6f43.png)  
L Install NVIDIA/apex to enable SyncBN  
  ![image](https://user-images.githubusercontent.com/56099627/78117392-95500600-7440-11ea-9fb6-3a02dd248e2c.png)  
  
## HRNet-Facial-Landmark-Detection  
https://github.com/HRNet/HRNet-Facial-Landmark-Detection  

This code is developed using on **Python 3.6 and PyTorch 1.0.0** on Ubuntu 16.04 with NVIDIA GPUs.  
HRNet-Facial-Landmark-Detection folder  
L Install dependencies  
  pip install -r requirements.txt  
  ![image](https://user-images.githubusercontent.com/56099627/78127392-0bf40000-744f-11ea-97b1-c7fb7186cfad.png) L dataset DOWNLOAD  
  https://github.com/jian667/face-dataset  
L test.py 진행 중 error: " scipy.misc import imresize " 만나면 아래 처럼 해결!  

    " scipy.misc import imresize "  에러가 발생한다면 scipy버전이 최신 버전이기 때문입니다. 
    1.3.0 이상 버전 부터 imresize를 제거 했기 때문에 로드할 수 없는 상태이구요 
    아나콘다 명령프롬프트(cmd)창을 열어서  명령어 : pip install scipy==1.1.0 
    
    onda install Scipy = 1.1.0 because imread has been deprecated in scipy 1.2.0+
  
------------------------------------------------------
## video-realtime poseEstimation  
https://github.com/lxy5513/videopose  

## TensorRT Pose Estimation
https://github.com/NVIDIA-AI-IOT/trt_pose  
