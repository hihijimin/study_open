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
