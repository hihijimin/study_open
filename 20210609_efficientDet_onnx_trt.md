## setup goal
onnx 와 tensorrt 생성을 위해 sota model 중 하난로 efficientDet 선정했고 onnx 및  tensorrt 적용해 보기 위해  

## install base on pytorch
참고: (EfficientDet.Pytorch) https://github.com/toandaominh1997/EfficientDet.Pytorch  
```
numpy 
pandas : ppip install pandas
torch : 1.3+
torchvision : 0.4+
pytoan : pip install pytoan
albumentations : pip install albumentations==0.5.2

opencv : pip install opencv-python
matplotlib : pip install matplotlib

```
## covert torch to onnx
참고: https://github.com/murdockhou/Yet-Another-EfficientDet-Pytorch-Convert-ONNX-TVM/  
efficientdet 모델을 onnx 으로 바꿔주는 깃허브  
convert/convert_onnx.py 으로 실행
```
import torch
#import yaml
from torch import nn
from backbone import EfficientDetBackbone
import numpy as np


# mean and std in RGB order, actually this part should remain unchanged as long as your dataset is similar to coco.
mean= [0.485, 0.456, 0.406]
std= [0.229, 0.224, 0.225]

# this is coco anchors, change it if necessary
anchors_scales= '[2 ** 0, 2 ** (1.0 / 3.0), 2 ** (2.0 / 3.0)]'
anchors_ratios= '[(1.0, 1.0), (1.4, 0.7), (0.7, 1.4)]'

# must match your dataset's category_id.
# category_id is one_indexed,
# for example, index of 'car' here is 2, while category_id of is 3
obj_list= ['person', 'bicycle', 'car', 'motorcycle', 'airplane', 'bus', 'train', 'truck', 'boat', 'traffic light',
           'fire hydrant', '', 'stop sign', 'parking meter', 'bench', 'bird', 'cat', 'dog', 'horse', 'sheep',
           'cow', 'elephant', 'bear', 'zebra', 'giraffe', '', 'backpack', 'umbrella', '', '', 'handbag', 'tie',
           'suitcase', 'frisbee', 'skis', 'snowboard', 'sports ball', 'kite', 'baseball bat', 'baseball glove',
           'skateboard', 'surfboard', 'tennis racket', 'bottle', '', 'wine glass', 'cup', 'fork', 'knife', 'spoon',
           'bowl', 'banana', 'apple', 'sandwich', 'orange', 'broccoli', 'carrot', 'hot dog', 'pizza', 'donut',
           'cake', 'chair', 'couch', 'potted plant', 'bed', '', 'dining table', '', '', 'toilet', '', 'tv',
           'laptop', 'mouse', 'remote', 'keyboard', 'cell phone', 'microwave', 'oven', 'toaster', 'sink',
           'refrigerator', '', 'book', 'clock', 'vase', 'scissors', 'teddy bear', 'hair drier',
           'toothbrush']
    
class Params:
    def __init__(self, project_file):
        self.params = yaml.safe_load(open(project_file).read())

    def __getattr__(self, item):
        return self.params.get(item, None)

device = torch.device('cuda:0')
#params = Params(f'projects/coco.yml')
model = EfficientDetBackbone(num_classes=len(obj_list), compound_coef=0, onnx_export=True,
                                 ratios=eval(anchors_ratios), scales=eval(anchors_scales)).to(device)

                    
model.backbone_net.model.set_swish(memory_efficient=False)

dummy_input = torch.randn((1,3,512,512), dtype=torch.float32).to(device)

model.load_state_dict(torch.load(f'weights/efficientdet-d0.pth'))

# opset_version can be changed to 10 or other number, based on your need
torch.onnx.export(model, dummy_input,
                  'weights/efficientdet-d0.onnx',
                  verbose=False,
                  #input_names=['data'],
                  opset_version=11)

## result compare torch and onnx
## torch predict shape : (1, 49104, 4)  
## onnx predict shape: (1, 49104, 4)  
```

## 생성한 onnx 으로 convert onnx to tensorrt
결과 에러메세지:  
```
&&&& RUNNING TensorRT.trtexec # /mmdetection/TensorRT-7.2.2.3/targets/x86_64-linux-gnu/bin/trtexec --onnx=weights/efficientdet-d0.pth_1_512_512.onnx --explicitBatch --saveEngine=efficientdet-d0.engine --workspace=2048 --fp16
[06/10/2021-07:04:39] [I] === Model Options ===
[06/10/2021-07:04:39] [I] Format: ONNX
[06/10/2021-07:04:39] [I] Model: weights/efficientdet-d0.pth_1_512_512.onnx
[06/10/2021-07:04:39] [I] Output:
[06/10/2021-07:04:39] [I] === Build Options ===
[06/10/2021-07:04:39] [I] Max batch: explicit
[06/10/2021-07:04:39] [I] Workspace: 2048 MiB
[06/10/2021-07:04:39] [I] minTiming: 1
[06/10/2021-07:04:39] [I] avgTiming: 8
[06/10/2021-07:04:39] [I] Precision: FP32+FP16
[06/10/2021-07:04:39] [I] Calibration: 
[06/10/2021-07:04:39] [I] Refit: Disabled
[06/10/2021-07:04:39] [I] Safe mode: Disabled
[06/10/2021-07:04:39] [I] Save engine: efficientdet-d0.engine
[06/10/2021-07:04:39] [I] Load engine: 
[06/10/2021-07:04:39] [I] Builder Cache: Enabled
[06/10/2021-07:04:39] [I] NVTX verbosity: 0
[06/10/2021-07:04:39] [I] Tactic sources: Using default tactic sources
[06/10/2021-07:04:39] [I] Input(s)s format: fp32:CHW
[06/10/2021-07:04:39] [I] Output(s)s format: fp32:CHW
[06/10/2021-07:04:39] [I] Input build shapes: model
[06/10/2021-07:04:39] [I] Input calibration shapes: model
[06/10/2021-07:04:39] [I] === System Options ===
[06/10/2021-07:04:39] [I] Device: 0
[06/10/2021-07:04:39] [I] DLACore: 
[06/10/2021-07:04:39] [I] Plugins:
[06/10/2021-07:04:39] [I] === Inference Options ===
[06/10/2021-07:04:39] [I] Batch: Explicit
[06/10/2021-07:04:39] [I] Input inference shapes: model
[06/10/2021-07:04:39] [I] Iterations: 10
[06/10/2021-07:04:39] [I] Duration: 3s (+ 200ms warm up)
[06/10/2021-07:04:39] [I] Sleep time: 0ms
[06/10/2021-07:04:39] [I] Streams: 1
[06/10/2021-07:04:39] [I] ExposeDMA: Disabled
[06/10/2021-07:04:39] [I] Data transfers: Enabled
[06/10/2021-07:04:39] [I] Spin-wait: Disabled
[06/10/2021-07:04:39] [I] Multithreading: Disabled
[06/10/2021-07:04:39] [I] CUDA Graph: Disabled
[06/10/2021-07:04:39] [I] Separate profiling: Disabled
[06/10/2021-07:04:39] [I] Skip inference: Disabled
[06/10/2021-07:04:39] [I] Inputs:
[06/10/2021-07:04:39] [I] === Reporting Options ===
[06/10/2021-07:04:39] [I] Verbose: Disabled
[06/10/2021-07:04:39] [I] Averages: 10 inferences
[06/10/2021-07:04:39] [I] Percentile: 99
[06/10/2021-07:04:39] [I] Dump refittable layers:Disabled
[06/10/2021-07:04:39] [I] Dump output: Disabled
[06/10/2021-07:04:39] [I] Profile: Disabled
[06/10/2021-07:04:39] [I] Export timing to JSON file: 
[06/10/2021-07:04:39] [I] Export output to JSON file: 
[06/10/2021-07:04:39] [I] Export profile to JSON file: 
[06/10/2021-07:04:39] [I] 
[06/10/2021-07:04:39] [I] === Device Information ===
[06/10/2021-07:04:39] [I] Selected Device: GeForce RTX 2080 Ti
[06/10/2021-07:04:39] [I] Compute Capability: 7.5
[06/10/2021-07:04:39] [I] SMs: 68
[06/10/2021-07:04:39] [I] Compute Clock Rate: 1.65 GHz
[06/10/2021-07:04:39] [I] Device Global Memory: 11016 MiB
[06/10/2021-07:04:39] [I] Shared Memory per SM: 64 KiB
[06/10/2021-07:04:39] [I] Memory Bus Width: 352 bits (ECC disabled)
[06/10/2021-07:04:39] [I] Memory Clock Rate: 7 GHz
[06/10/2021-07:04:39] [I] 
----------------------------------------------------------------
Input filename:   weights/efficientdet-d0.pth_1_512_512.onnx
ONNX IR version:  0.0.6
Opset version:    11
Producer name:    pytorch
Producer version: 1.7
Domain:           
Model version:    0
Doc string:       
----------------------------------------------------------------
[06/10/2021-07:04:50] [W] [TRT] onnx2trt_utils.cpp:220: Your ONNX model has been generated with INT64 weights, while TensorRT does not natively support INT64. Attempting to cast down to INT32.
[06/10/2021-07:04:50] [W] [TRT] onnx2trt_utils.cpp:246: One or more weights outside the range of INT32 was clamped
ERROR: builtin_op_importers.cpp:2249 In function importPad:
[8] Assertion failed: inputs.at(1).is_weights()
[06/10/2021-07:04:50] [E] Failed to parse onnx file
[06/10/2021-07:04:50] [E] Parsing model failed
[06/10/2021-07:04:50] [E] Engine creation failed
[06/10/2021-07:04:50] [E] Engine set up failed
&&&& FAILED TensorRT.trtexec # /mmdetection/TensorRT-7.2.2.3/targets/x86_64-linux-gnu/bin/trtexec --onnx=weights/efficientdet-d0.pth_1_512_512.onnx --explicitBatch --saveEngine=efficientdet-d0.engine --workspace=2048 --fp16
```
[8] Assertion failed: inputs.at(1).is_weights()  
-> I am afraid, but TRT currently does not support convolutions where the weights are tensors.  [지원불가 소개 링크](https://forums.developer.nvidia.com/t/assertion-failed-inputs-at-1-is-weights/153445/2)  

[tensorrt 에서 지원되는 Caffe, TensorFlow, ONNX 연산들](https://docs.nvidia.com/deeplearning/tensorrt/support-matrix/index.html)
