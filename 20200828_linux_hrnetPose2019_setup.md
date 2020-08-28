### HRnet2019 pose-estimation setup
https://github.com/leoxiaobin/deep-high-resolution-net.pytorch  
1. python & torchvision 설치  
(Install pytorch >= v1.0.0)  
pip 설치 $ pip install torch==1.5.0 torchvision==0.6.0  
2. git clone 이후 requirements 설치 
requirements.txt 그대로 설치  
$ pip install -r requirements.txt  
```
EasyDict==1.7
opencv-python==3.4.1.15
shapely==1.6.4
Cython
scipy
pandas
pyyaml
json_tricks
scikit-image
yacs>=0.1.5
tensorboardX==1.6
```
3. Make lib & Install COCOAPI  
Make libs:  
```
cd ${POSE_ROOT}/lib
make
```
Install COCOAPI:  
```
$ git clone https://github.com/cocodataset/cocoapi.git $COCOAPI
$ cd cocoapi/PythonAPI
$ make
$ make install
$ python setup.py install --user
```
## inference 실행 
https://github.com/leoxiaobin/deep-high-resolution-net.pytorch/tree/master/demo  
```
parser.add_argument('--cfg', type=str, default='./experiments/coco/hrnet/w32_384x288_adam_lr1e-3.yaml')  
--writeBoxFrames TEST.MODEL_FILE ./models/pytorch/pose_coco/pose_hrnet_w32_384x288.pth
```
