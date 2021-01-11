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
