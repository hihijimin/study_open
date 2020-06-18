## pytorch-based yolo3
simple_HRNetpose에서 yolo3 모델을 업데이트 하기 위해서 pytorch-based yolo 환경 셋팅, detector 실행, training 하기 위한 준비들  
https://github.com/eriklindernoren/PyTorch-YOLOv3  

### annotation 준비
https://github.com/AlexeyAB/Yolo_mark/issues/60  
https://github.com/AlexeyAB/darknet#how-to-train-to-detect-your-custom-objects  
`.txt`-file for each `.jpg`-image-file - in the same directory and with the same name, but with `.txt`-extension, and put to file: object number and object coordinates on this image, for each object in new line: `<object-class> <x> <y> <width> <height>`  
Where:

- `<object-class>` - integer number of object from 0 to (classes-1)
- `<x> <y> <width> <height>` - float values relative to width and height of image, it can be equal from (0.0 to 1.0]
- for example: `<x> = <absolute_x> / <image_width> or <height> = <absolute_height> / <image_height>`
- atention: `<x> <y>` - are center of rectangle (are not top-left corner)
  
For example for `img1.jpg` you will be created `img1.txt` containing:
```
1 0.716797 0.395833 0.216406 0.147222
0 0.687109 0.379167 0.255469 0.158333
1 0.420312 0.395833 0.140625 0.166667
```
