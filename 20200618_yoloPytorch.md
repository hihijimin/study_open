## pytorch-based yolo3
simple_HRNetpose에서 yolo3 모델을 업데이트 하기 위해서 pytorch-based yolo 환경 셋팅, detector 실행, training 하기 위한 준비들  
https://github.com/eriklindernoren/PyTorch-YOLOv3  

- $ pip install -r requirements.txt 
requirements.txt 에서 빼서 따로 torch & torchvision 설치해줌 $ 
```
numpy
matplotlib
tensorflow
tensorboard
terminaltables
pillow
tqdm

Successfully installed absl-py-0.9.0 astunparse-1.6.3 cachetools-4.1.0 chardet-3.0.4 gast-0.3.3 google-auth-1.17.2 google-auth-oauthlib-0.4.1 google-pasta-0.2.0 grpcio-1.29.0 h5py-2.10.0 idna-2.9 importlib-metadata-1.6.1 keras-preprocessing-1.1.2 markdown-3.2.2 oauthlib-3.1.0 opt-einsum-3.2.1 pyasn1-0.4.8 pyasn1-modules-0.2.8 requests-2.24.0 requests-oauthlib-1.3.0 rsa-4.6 tensorboard-2.2.2 tensorboard-plugin-wit-1.6.0.post3 tensorflow-2.2.0 tensorflow-estimator-2.2.0 termcolor-1.1.0 terminaltables-3.1.0 urllib3-1.25.9 werkzeug-1.0.1 wrapt-1.12.1 zipp-3.1.0
```



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

### 학습
error message 1: **module 'tensorboard.summary._tf.summary' has no attribute 'FileWriter'**
```
Traceback (most recent call last):
  File "/media/humani/5c5d0d82-9f8b-48ea-ae45-a8d930d14008/PyTorch-YOLOv3/train_modify.py", line 42, in <module>
    logger = Logger("logs")
  File "/media/humani/5c5d0d82-9f8b-48ea-ae45-a8d930d14008/PyTorch-YOLOv3/utils/logger.py", line 7, in __init__
    self.writer = tf.summary.FileWriter(log_dir)
AttributeError: module 'tensorboard.summary._tf.summary' has no attribute 'FileWriter'
```
해결: https://github.com/eriklindernoren/PyTorch-YOLOv3/issues/327 참고  
try to use **tf.summary.create_file_writer('log_dir')** in tensorflow 2.0  
(logger.py 원본) self.writer = tf.summary.FileWriter(log_dir)  
--> (logger.py 바꾸기) self.writer = tf.summary.create_file_writer('log_dir')  

```
import tensorflow as tf

class Logger(object):
    def __init__(self, log_dir):
        """Create a summary writer logging to log_dir."""
        # self.writer = tf.summary.FileWriter(log_dir)
        self.writer = tf.summary.create_file_writer(log_dir)

    def scalar_summary(self, tag, value, step):
        """Log a scalar variable."""
        with self.writer.as_default():
            tf.summary.scalar(tag, value, step=step)
            self.writer.flush()
        # summary = tf.Summary(value=[tf.Summary.Value(tag=tag, simple_value=value)])
        # self.writer.add_summary(summary, step)

    def list_of_scalars_summary(self, tag_value_pairs, step):
        """Log scalar variables."""
        with self.writer.as_default():
            for tag, value in tag_value_pairs:
                tf.summary.scalar(tag, value, step=step)
            self.writer.flush()
        # summary = tf.Summary(value=[tf.Summary.Value(tag=tag, simple_value=value) for tag, value in tag_value_pairs])
        # self.writer.add_summary(summary, step)
```
