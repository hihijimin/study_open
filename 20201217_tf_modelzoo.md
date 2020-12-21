### object detection api 
https://github.com/tensorflow/models/tree/master/research/object_detection  

### 환경 셋업
- tensorflow2 으로 환경 셋업 하기 위해 
https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2.md
```
### Installation
$ git clone https://github.com/tensorflow/models.git

### Python Package Installation
$ cd models/research
# Compile protos.
protoc object_detection/protos/*.proto --python_out=.
# Install TensorFlow Object Detection API.
cp object_detection/packages/tf2/setup.py .
python -m pip install --use-feature=2020-resolver .
# Test the installation.
python object_detection/builders/model_builder_tf2_test.py1
```
![image](https://user-images.githubusercontent.com/56099627/102451425-ced2ab00-407b-11eb-943e-d8ba621a399c.png)  
![image](https://user-images.githubusercontent.com/56099627/102451488-ead64c80-407b-11eb-99f4-9358b951d0e6.png)  
![image](https://user-images.githubusercontent.com/56099627/102451547-08a3b180-407c-11eb-8f3c-14d3555b6402.png)  

### pip install tensorflow==2.3
cuda-10.1, cudnn-7.6버전 설치 하여 pip install tensoflow==2.1 을 설치하였음
: cuda_10.1.105_418.39_linux.run, cudnn-10.1-linux-x64-v7.6.5.32.tgz  
cuda - tensorflow 호환 버전 확인 링크: https://www.tensorflow.org/install/source?hl=ko  
--> 근데 pip install tensorflow==2.3 설치해야만 다른 패키지 실행 가능함

### train 전에 TfRecords 만들기
https://github.com/mwindowshz/YoloToTfRecords  
: yolo format -> xml format -> csv format -> tfrecord format  

### train 하기 위한 model download(pipline_config)
https://becominghuman.ai/tensorflow-object-detection-api-tutorial-training-and-evaluating-custom-object-detector-ed2594afcf73  
1. 원하는 모델 적당한 위치에 다운로드 하기  
https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md  
2. pipline_config 수정하기  
EfficientDet D0 512x512 모델 다운로드 받은 후, 클래스 바꾸기(**num_classes: 1**), **fine_tune_checkpoint: "custom_dir/efficientdet_d0_coco17_tpu-32/checkpoint/ckpt-0"**, **fine_tune_checkpoint_type: "detection"**
3. research/object_detection/model_main_tf2.py 수정하기  
: tensorflow v 2.3 환경에서 model_main.py 이거보단 model_main_tf2.py 이거 실행하길 추천!  
: **'pipeline_config_path', '../models/ssd_mobilenet_v1_fpn_640x640_coco17_tpu-8/pipeline.config'**  
: **'model_dir', '../models/ssd_mobilenet_v1_fpn_640x640_coco17_tpu-8/saved_model.pb'**  
4. lable_map(.pbtxt) 파일 만들기  
```
item  {
  id: 1
  name: 'person'
}
```

### tensorflow 실행 중 발생 하는 에러
```
2020-12-17 17:01:05.249234: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libnvinfer.so.6'; dlerror: libnvinfer.so.6: cannot open shared object file: No such file or directory
2020-12-17 17:01:05.249308: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libnvinfer_plugin.so.6'; dlerror: libnvinfer_plugin.so.6: cannot open shared object file: No such file or directory
2020-12-17 17:01:05.249316: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:30] Cannot dlopen some TensorRT libraries. If you would like to use Nvidia GPU with TensorRT, please make sure the missing libraries mentioned above are installed properly.
```
--> (https://qastack.kr/programming/60368298/could-not-load-dynamic-library-libnvinfer-so-6  
이것은 오류가 아니라 경고입니다. 여전히 TensorFlow를 사용할 수 있습니다. 공유 라이브러리 libnvinfer와는 libnvinfer_plugin선택 사항이며 엔비디아의 TensorRT 기능을 사용하는 경우에만 필요합니다.
```
시스템에 다음 NVIDIA® 소프트웨어가 설치되어 있어야합니다.

NVIDIA® GPU 드라이버 —CUDA 10.1에는 418.x 이상이 필요합니다.
CUDA® 툴킷 —TensorFlow는 CUDA 10.1을 지원합니다 (TensorFlow> = 2.1.0)
CUPTI는 CUDA 툴킷과 함께 제공됩니다.
cuDNN SDK (> = 7.6)
(선택 사항) 일부 모델에서 유추에 대한 대기 시간 및 처리량을 향상시키는 TensorRT 6.0
다음 명령을 사용하여 Ubuntu 18.04에이를 설치할 수 있습니다 ( TensorFlow 설명서 에서 가져옴 ).

# Add NVIDIA package repositories
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.1.243-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804_10.1.243-1_amd64.deb
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
sudo apt-get update
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
sudo apt install ./nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
sudo apt-get update

# Install NVIDIA driver
sudo apt-get install --no-install-recommends nvidia-driver-430
# Reboot. Check that GPUs are visible using the command: nvidia-smi

# Install development and runtime libraries (~4GB)
sudo apt-get install --no-install-recommends \
    cuda-10-1 \
    libcudnn7=7.6.4.38-1+cuda10.1  \
    libcudnn7-dev=7.6.4.38-1+cuda10.1


# Install TensorRT. Requires that libcudnn7 is installed above.
sudo apt-get install -y --no-install-recommends libnvinfer6=6.0.1-1+cuda10.1 \
    libnvinfer-dev=6.0.1-1+cuda10.1 \
    libnvinfer-plugin6=6.0.1-1+cuda10.1
```
### 에러
```
AttributeError: module 'tensorflow' has no attribute 'python_io'
```
--> (해결) https://github.com/datitran/raccoon_dataset/issues/90  
**tf.compat.v1.python_io**
![image](https://user-images.githubusercontent.com/56099627/102461457-bbc7d700-408b-11eb-88ed-34d298d42233.png)  
