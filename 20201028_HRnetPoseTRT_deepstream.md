docker deepstream-5.0 이미지 받기  
ㄴ torch2trt 깃헙 셋팅  
ㄴ trt_pose 깃헙 세팅: openpose 기반  

https://github.com/NVIDIA-AI-IOT/trt_pose  
trt_pose 할때 필요한 코드:  
https://spyjetson.blogspot.com/2019/12/jetsonnano-human-pose-estimation-using.html  

onnx convert  
해외 블로그 https://satyajitghana.medium.com/human-pose-estimation-and-quantization-of-pytorch-to-onnx-models-a-detailed-guide-b9c91ddc0d9f  
pytorch 공식 블로그 https://pytorch.org/tutorials/advanced/super_resolution_with_onnxruntime.html  
한글 블로그 https://tutorials.pytorch.kr/advanced/super_resolution_with_onnxruntime.html  

deepstream_pose_estimation  
https://github.com/NVIDIA-AI-IOT/deepstream_pose_estimation  

higher-HRnet pose(onnx 있음)  
https://github.com/luohuan2uestc/pose-multi/blob/master/tools/export_to_onnx.py  

nvidia에서 제공하는 tensorrt 실행 가이드
https://docs.nvidia.com/deeplearning/tensorrt/api/python_api/gettingStarted.html

trt_pose  
/trt_pose/utils/export_for_isaac.py 실행코드  
python3 trt_pose/utils/export_for_isaac.py --input_checkpoint resnet18_baseline_att_224x224_A_epoch_249.pth --input_model resnet18_baseline_att --input_topology tasks/human_pose/human_pose.json --input_width 224 --input_height 224 --output_model resnet18_baseline_att_224x224_A_epoch_249.onnx  
