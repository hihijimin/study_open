## simple HRnet 설치
빠른 video_demo을 위해~~ 설치.  
HRnet2019버전으로 pose estimation 한 것임  
https://github.com/stefanopini/simple-HRNet  
  
1. 설치 시작  
1-0. pytorch, torchvision 설치  
onlyCPU  
$ conda install pytorch==1.5.0 torchvision==0.6.0 cpuonly -c pytorch   
![image](https://user-images.githubusercontent.com/56099627/84871915-1b80fd80-b0bc-11ea-822f-bde89796613c.png)  
conda 연동 설치  
$ conda install pytorch torchvision cudatoolkit=10.0  
![image](https://user-images.githubusercontent.com/56099627/84872136-761a5980-b0bc-11ea-8d97-c9ba6b3a2e04.png)  
pip 설치  
$ pip install torch==1.5.0 torchvision==0.6.0  
![image](https://user-images.githubusercontent.com/56099627/84872273-a530cb00-b0bc-11ea-8f47-0a561c18335d.png)  
pip + cuda 설치(원하는 버전: torch==1.5.0 torchvision==0.6.0)  
$ pip install torch==1.5.0+cu100 torchvision==0.6.0+cu100 -f https://download.pytorch.org/whl/torch_stable.html  
![image](https://user-images.githubusercontent.com/56099627/84872415-d7dac380-b0bc-11ea-81b3-d570d39afd0c.png)  
![image](https://user-images.githubusercontent.com/56099627/84872612-12dcf700-b0bd-11ea-9556-dfbd9146cde2.png)  
-> 에러발생: 설치된 cuda 버전과 설치하고자 하는  torch 버전이 맞지 않다는 메세지  
pip + cuda10.0 설치 (원하는 버전 수정: torch==1.4.0 torchvision==0.5.0)  
$ pip install torch==1.4.0+cu100 torchvision==0.5.0+cu100 -f https://download.pytorch.org/whl/torch_stable.html  
-> 안정적으로 설치됨  
![image](https://user-images.githubusercontent.com/56099627/84872856-5f283700-b0bd-11ea-8197-c3463468bfe8.png)  
![image](https://user-images.githubusercontent.com/56099627/84872938-75ce8e00-b0bd-11ea-80ba-0706072737d1.png)  

    <참고>  
    https://varhowto.com/how-to-install-pytorch-with-cuda-10-0/

    1. Check if CUDA 10.0 is installed
    cat /usr/local/cuda/version.txt

    2. [For pip] Run pip install with specified version and -f
    pip install torch==1.5.0+cu100 torchvision==0.6.0+cu100 -f https://download.pytorch.org/whl/torch_stable.html

    3. [For conda] Run conda install with cudatoolkit
    conda install pytorch torchvision cudatoolkit=10.0 -c pytorch

    4. Verify PyTorch is installed
    Run Python with

    import torch
    x = torch.rand(5, 3)
    print(x)

    5. Verify PyTorch is using CUDA 10.0
    Run Python with

  import torch
  torch.cuda.is_available()
  
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
  
$ sh download_weights.sh  
"Download the pre-trained weights running the script **download_weights.sh from the weights folder**"  
![image](https://user-images.githubusercontent.com/56099627/81368588-1a5ac900-912b-11ea-90e4-5b9cad98d0ac.png)  
  
## 에러발생
1. FileNotFoundError: [Errno 2] No such file or directory: 'ffprobe': 'ffprobe'

  /home/jimin/anaconda3/envs/simplepose/bin/python /media/jimin/D/simple-HRNet/scripts/live-demo.py
  Traceback (most recent call last):
    File "/media/jimin/D/simple-HRNet/scripts/live-demo.py", line 185, in <module>
      main(**args.__dict__)
    File "/media/jimin/D/simple-HRNet/scripts/live-demo.py", line 35, in main
      rotation_code = check_video_rotation(filename)
    File "/media/jimin/D/simple-HRNet/misc/visualization.py", line 268, in check_video_rotation
      meta_dict = ffmpeg.probe(filename)
    File "/home/jimin/anaconda3/envs/simplepose/lib/python3.6/site-packages/ffmpeg/_probe.py", line 20, in probe
      p = subprocess.Popen(args, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
    File "/home/jimin/anaconda3/envs/simplepose/lib/python3.6/subprocess.py", line 729, in __init__
      restore_signals, start_new_session)
    File "/home/jimin/anaconda3/envs/simplepose/lib/python3.6/subprocess.py", line 1364, in _execute_child
      raise child_exception_type(errno_num, err_msg, err_filename)
  FileNotFoundError: [Errno 2] No such file or directory: 'ffprobe': 'ffprobe'

  Process finished with exit code 1

참고사이트:
https://stackoverflow.com/questions/57350259/filenotfounderror-errno-2-no-such-file-or-directory-ffprobe-ffprobe 

해결  
https://github.com/adaptlearning/adapt_authoring/wiki/Installing-FFmpeg  
우분투에서 FFmpeg 설치  
$ sudo add-apt-repository ppa:mc3man/trusty-media  
$ sudo apt-get update  
$ sudo apt-get install ffmpeg  
$ sudo apt-get install frei0r-plugins  
우분투에서 ffprobe 설치  
$ pip install ffprobe  
![image](https://user-images.githubusercontent.com/56099627/81368771-9ce38880-912b-11ea-92a9-6c03c9f9d744.png)  
