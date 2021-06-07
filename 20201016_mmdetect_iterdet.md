공식코드사이트: https://github.com/open-mmlab/mmdetection  
설치가이드: https://mmdetection.readthedocs.io/en/latest/install.html  

### set-up
1. pytorch cuda 버전에 맞게 설치  
pytorch 1.6, torchvision 7.0 : 공식 pytorch 사이트 들어가서 pytorch, torchvision 설치 할것  
![image](https://user-images.githubusercontent.com/56099627/96215112-0a87c080-0fb8-11eb-96d5-41cae6caad67.png)  

2. mmcv 패키지 설치(cuda 버전 맞춰 설치)  
https://github.com/open-mmlab/mmcv#install-with-pip  
![image](https://user-images.githubusercontent.com/56099627/96215220-5a668780-0fb8-11eb-940b-2696a5b71dce.png)  
![image](https://user-images.githubusercontent.com/56099627/104157957-a007e480-542f-11eb-873d-c937797af50a.png)  


3. build  
레파지토리 다운로드 한 후, **pip install -v -e .** 명령으로 빌드하기  
```
git clone https://github.com/open-mmlab/mmdetection.git
cd mmdetection
pip install -r requirements/build.txt (cython, numpy 이 있다면 생략)
pip install -v -e .  # or "python setup.py develop"
```
1  
![image](https://user-images.githubusercontent.com/56099627/97129753-07908b00-1783-11eb-9eb2-eaecf05f6855.png)  
2  
![image](https://user-images.githubusercontent.com/56099627/97129821-3149b200-1783-11eb-9f21-393cc065daaa.png)  
3  
![image](https://user-images.githubusercontent.com/56099627/97129879-4de5ea00-1783-11eb-97f3-c2cc823ebfe6.png)  
4  
![image](https://user-images.githubusercontent.com/56099627/97129933-6eae3f80-1783-11eb-846d-f8a1d88b6b6f.png)  
5  
![image](https://user-images.githubusercontent.com/56099627/97129981-8c7ba480-1783-11eb-86c7-2cfee1ab551d.png)  
6  
![image](https://user-images.githubusercontent.com/56099627/97130065-b7fe8f00-1783-11eb-965f-46280d2f4517.png)  
7  
![image](https://user-images.githubusercontent.com/56099627/97130121-d5335d80-1783-11eb-9663-ec7380cdad59.png)  

## 실행
./demo/image_demo.py 에서 잘 실행되는지 보기  
```
parser.add_argument('--img', help='Image file', type=str, default='')
parser.add_argument('--config', help='Config file', type=str, default='')
parser.add_argument('--checkpoint', help='Checkpoint file', type=str, default='')
parser.add_argument('--device', default='cuda:0', help='Device used for inference')
parser.add_argument('--score-thr', type=float, default=0.3, help='bbox score threshold')
```
## mmdetection docker for tensorrt
https://github.com/open-mmlab/mmdetection/blob/master/docs/get_started.md  
0. docker file
```
# nvidia-driver 450, cuda 11, cudnn 8 환경에서 mmcv-full 파키지 설치하기  
ARG PYTORCH="1.7.0"
ARG CUDA="11.0"
ARG CUDNN="8"

FROM pytorch/pytorch:${PYTORCH}-cuda${CUDA}-cudnn${CUDNN}-devel

ENV TORCH_CUDA_ARCH_LIST="6.0 6.1 7.0+PTX"
ENV TORCH_NVCC_FLAGS="-Xfatbin -compress-all"
ENV CMAKE_PREFIX_PATH="$(dirname $(which conda))/../"

RUN apt-get update && apt-get install -y ffmpeg libsm6 libxext6 git ninja-build libglib2.0-0 libsm6 libxrender-dev libxext6 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install MMCV
RUN pip install mmcv-full==latest+torch1.7.0+cu110 -f https://openmmlab.oss-accelerate.aliyuncs.com/mmcv/dist/index.html

# Install MMDetection
RUN conda clean --all
RUN git clone https://github.com/open-mmlab/mmdetection.git /mmdetection
WORKDIR /mmdetection
ENV FORCE_CUDA="1"
RUN pip install -r requirements/build.txt
RUN pip install --no-cache-dir -e .

# Update apt packages
RUN apt update
RUN apt upgrade -y

# Install vim
RUN apt install vim -y
```
1. mmdetection docker image download: $ docker build -t mmdetection docker/  
2. Tensorrt (.tar)다운로드 후, mmdetection dir 안에 넣어주기
3. mmcv download : https://github.com/open-mmlab/mmcv/blob/master/docs/tensorrt_plugin.md  
```
clone $ git clone https://github.com/open-mmlab/mmcv.git

Install TensorRT
Download the corresponding TensorRT build from NVIDIA Developer Zone.

For example, for Ubuntu 16.04 on x86-64 with cuda-10.2, the downloaded file is TensorRT-7.2.1.6.Ubuntu-16.04.x86_64-gnu.cuda-10.2.cudnn8.0.tar.gz.

Then, install as below:

$ cd ~/Downloads
$ tar -xvzf TensorRT-7.2.2.3.Ubuntu-18.04.x86_64-gnu.cuda-11.0.cudnn8.0.tar.gz
export TENSORRT_DIR=`pwd`/TensorRT-7.2.2.3
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$TENSORRT_DIR/lib
Install python packages: tensorrt, graphsurgeon, onnx-graphsurgeon

$ pip install $TENSORRT_DIR/python/tensorrt-7.2.2.3-cp38-none-linux_x86_64.whl
$ pip install $TENSORRT_DIR/onnx_graphsurgeon/onnx_graphsurgeon-0.2.6-py2.py3-none-any.whl
$ pip install $TENSORRT_DIR/graphsurgeon/graphsurgeon-0.4.5-py2.py3-none-any.whl
For more detailed infomation of installing TensorRT using tar, please refer to Nvidia' website.

Build on Linux
$ cd mmcv # to MMCV root directory
$ MMCV_WITH_OPS=1 MMCV_WITH_TRT=1 pip install -e .
```
4. 실행 : docker run --gpus all --shm-size=8g -it --name onnxtrt -p 9000:9000 -v "/home/jimin/D/mmdetection_new":"/mmdetection" mmdetection_cuda11 /bin/bash 

## mmdetect 에 onnx 실행하기
[reference: mmdetect onnx doc](https://github.com/open-mmlab/mmdetection/blob/master/docs/tutorials/pytorch2onnx.md#list-of-supported-models-exportable-to-onnx)
Install onnx and onnxruntime

  ```shell
  pip install onnx onnxruntime
  ```
List of supported models exportable to ONNX  
The table below lists the models that are guaranteed to be exportable to ONNX and runnable in ONNX Runtime.  

|    Model     |                               Config                                | Dynamic Shape | Batch Inference |                                     Note                                      |
| :----------: | :-----------------------------------------------------------------: | :-----------: | :-------------: | :---------------------------------------------------------------------------: |
|     FCOS     |      `configs/fcos/fcos_r50_caffe_fpn_gn-head_4x4_1x_coco.py`       |       Y       |        Y        |                                                                               |
|     FSAF     |               `configs/fsaf/fsaf_r50_fpn_1x_coco.py`                |       Y       |        Y        |                                                                               |
|  RetinaNet   |          `configs/retinanet/retinanet_r50_fpn_1x_coco.py`           |       Y       |        Y        |                                                                               |
|     SSD      |                    `configs/ssd/ssd300_coco.py`                     |       Y       |        Y        |                                                                               |
|    YOLOv3    |         `configs/yolo/yolov3_d53_mstrain-608_273e_coco.py`          |       Y       |        Y        |                                                                               |
| Faster R-CNN |        `configs/faster_rcnn/faster_rcnn_r50_fpn_1x_coco.py`         |       Y       |        Y        |                                                                               |
|  Mask R-CNN  |          `configs/mask_rcnn/mask_rcnn_r50_fpn_1x_coco.py`           |       Y       |        Y        |                                                                               |
|  CornerNet   | `configs/cornernet/cornernet_hourglass104_mstest_10x5_210e_coco.py` |       Y       |        N        | no flip, no batch inference, tested with torch==1.7.0 and onnxruntime==1.5.1. |
 

## iterdet docker 예시
$ docker run --gpus all --shm-size=8g -it --name iterdet_jm -p 8888:8888 -v "/home/jimin/HDD2/DB":"/iterdet/DB" iterdet /bin/bash  
$ pip install notebook  
$ jupyter notebook --ip=0.0.0.0 -port=8888 --allow-root  

$ docker run --gpus all -it --privileged --ipc=host -v [Ai 디렉토리]:/workspace -w /workspace -p 8080:8080 --name iter_pose_trt -v [동영상 디렉토리]:/workspace/DB -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY hict/aipose:20210308  
$ docker run -it --gpus all --privileged --ipc=host --shm-size=8g -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY --name torch2onnx -v /home/jimin/HDD1/iterdet:/iterdet --ip 0.0.0.0 -p 9000:9000 iterdet /bin/bash
```
참고
https://soyoung-new-challenge.tistory.com/70

--shm-size 의미: shared memory 설정
따로 추가 설정을 하지 않을 시 기본 --shm-size = 4mb이다
- 기본 설정으로 딥러닝 모델 학습시 아래와 같은 insufficient shared memory 에러 발생
"[ERROR: Unexpected bus error encountered in worker. This might be caused by insufficient shared memory]"

- 여기서는 --shm-size=8G 로 설정
$ docker run --name deepmodel -ti --shm-size=8G -v [공유파일설정] [이미지_이름]:[이미지_태그]
- 위와 같이 재 설정 해주면 에러 없이 실행 가능
```
## train 
https://github.com/lesliejackson/PyTorch-Distributed-Training  
multi-gpu 사용하여 ~  
$ python -m torch.distributed.launch --nproc_per_node = ngpus --master_port = 29500 ./tools/train.py  

## train loss 확인(seaborn, tensorboard)
- seaborn 을 사용하여 train loss 확인  
  - pip install seaborn  
$ python ./tools/analyze_logs.py plot_curve [log 경로: ex) 20210119_133603.log.json] --keys loss  
- tensorboard  
  - pip install tensorboard==2.2, tensorflow==2.2  
  - config 파일에 옵션 추가하기(아래)  
```
log_config = dict(
    interval=50,
    hooks=[
        dict(type='TextLoggerHook'),
        dict(type='TensorboardLoggerHook')
    ])
```
