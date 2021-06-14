https://github.com/DeNA/Chainer_Realtime_Multi-Person_Pose_Estimation  
  
jimin@jimin-MS-7C13:/media/jimin/D$ git clone https://github.com/DeNA/Chainer_Realtime_Multi-Person_Pose_Estimation.git  
(tfpose1) jimin@jimin-MS-7C13:~/anaconda3/bin$ pip install chainer
(tfpose1) jimin@jimin-MS-7C13:~/anaconda3/bin$ conda install -c conda-forge matplotlib
(tfpose1) jimin@jimin-MS-7C13:/media/jimin/D/Chainer_Pose/models$ wget http://posefs1.perception.cs.cmu.edu/OpenPose/models/pose/coco/pose_iter_440000.caffemodel  
(tfpose1) jimin@jimin-MS-7C13:/media/jimin/D/Chainer_Pose/models$ wget http://posefs1.perception.cs.cmu.edu/OpenPose/models/face/pose_iter_116000.caffemodel  
(tfpose1) jimin@jimin-MS-7C13:/media/jimin/D/Chainer_Pose/models$ wget http://posefs1.perception.cs.cmu.edu/OpenPose/models/hand/pose_iter_102000.caffemodel  
  
(tfpose1) jimin@jimin-MS-7C13:/media/jimin/D/Chainer_Pose/models$ python convert_model.py posenet pose_iter_440000.caffemodel coco_posenet.npz  
(tfpose1) jimin@jimin-MS-7C13:/media/jimin/D/Chainer_Pose/models$ python convert_model.py facenet pose_iter_116000.caffemodel facenet.npz  
(tfpose1) jimin@jimin-MS-7C13:/media/jimin/D/Chainer_Pose/models$ python convert_model.py handnet pose_iter_102000.caffemodel handnet.npz  
  
test-cpu  
(tfpose1) jimin@jimin-MS-7C13:/media/jimin/D/Chainer_Pose$ python pose_detector.py posenet models/coco_posenet.npz --img data/person.png  
test-gpu  
(tfpose1) jimin@jimin-MS-7C13:/media/jimin/D/Chainer_Pose$ python pose_detector.py posenet models/coco_posenet.npz --img data/person.png --gpu 0  
RuntimeError: CUDA environment is not correctly set up  
(see https://github.com/chainer/chainer#installation).No module named 'cupy'  
  
solution for No module named 'cupy'  
![image](https://user-images.githubusercontent.com/56099627/77288549-6ab4cd80-6d1b-11ea-8da9-7d0398483d8d.png)  
![image](https://user-images.githubusercontent.com/56099627/77288598-87e99c00-6d1b-11ea-85b9-21d3d5fc5a91.png)  
![image](https://user-images.githubusercontent.com/56099627/77288687-b1a2c300-6d1b-11ea-8899-8efb574ac60f.png)  
