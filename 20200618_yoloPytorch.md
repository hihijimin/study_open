## pytorch-based yolo3
simple_HRNetpose에서 yolo3 모델을 업데이트 하기 위해서 pytorch-based yolo 환경 셋팅, detector 실행, training 하기 위한 준비들  
https://github.com/eriklindernoren/PyTorch-YOLOv3  

### annotation 준비
https://github.com/AlexeyAB/Yolo_mark/issues/60  
https://github.com/AlexeyAB/darknet#how-to-train-to-detect-your-custom-objects  
.txt-file for each .jpg-image-file - in the same directory and with the same name, but with .txt-extension, and put to file: object number and object coordinates on this image, for each object in new line: <object-class> <x> <y> <width> <height>  
