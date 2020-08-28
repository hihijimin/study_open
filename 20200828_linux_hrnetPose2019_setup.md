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
### inference 실행 
https://github.com/leoxiaobin/deep-high-resolution-net.pytorch/tree/master/demo  
```
parser.add_argument('--cfg', type=str, default='./experiments/coco/hrnet/w32_384x288_adam_lr1e-3.yaml')  
--writeBoxFrames TEST.MODEL_FILE ./models/pytorch/pose_coco/pose_hrnet_w32_384x288.pth
```

### inference 실행시 warning 문제 해결
```
/home/jimin/anaconda3/envs/hrnet_pose/lib/python3.6/site-packages/torchvision/ops/poolers.py:216: UserWarning: This overload of nonzero is deprecated:
	nonzero(Tensor input, *, Tensor out)
Consider using one of the following signatures instead:
	nonzero(Tensor input, *, bool as_tuple) (Triggered internally at  /pytorch/torch/csrc/utils/python_arg_parser.cpp:766.)
  idx_in_level = torch.nonzero(levels == level).squeeze(1)
```
**해결방법:**  
https://blog.csdn.net/dong_liuqi/article/details/106526403  

1. /home/jimin/anaconda3/envs/hrnet_pose/lib/python3.6/site-packages/torchvision/ops/boxes.py:216:  
**keep = keep.nonzero().squeeze(1) ==> keep = keep.nonzero(as_tuple=False).squeeze(1)**  

2. /home/jimin/anaconda3/envs/hrnet_pose/lib/python3.6/site-packages/torchvision/ops/poolers.py:216:  
**idx_in_level = torch.nonzero(levels == level).squeeze(1) ==> idx_in_level = torch.nonzero(levels == level, as_tuple=False).squeeze(1)**  

3. /home/jimin/anaconda3/envs/hrnet_pose/lib/python3.6/site-packages/torchvision/models/detection/roi_heads.py:703:  
**inds = torch.nonzero(scores > self.score_thresh).squeeze(1) ==> inds = torch.nonzero(scores > self.score_thresh, as_tuple=False).squeeze(1)**  
