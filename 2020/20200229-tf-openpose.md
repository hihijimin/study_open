https://github.com/ildoonet/tf-pose-estimation 을 보고 설치하기!  

![image](https://user-images.githubusercontent.com/56099627/75567025-23c51680-5a94-11ea-9a4e-1cc584f74771.png)  
![image](https://user-images.githubusercontent.com/56099627/75567086-49eab680-5a94-11ea-97cf-1dcc5376972b.png)  
![image](https://user-images.githubusercontent.com/56099627/75567157-65ee5800-5a94-11ea-94ac-cc57c07c2841.png)  
![image](https://user-images.githubusercontent.com/56099627/75567217-7b638200-5a94-11ea-94a4-0200627c0c02.png)  
![image](https://user-images.githubusercontent.com/56099627/75567267-93d39c80-5a94-11ea-93c6-393f70965aca.png)  
![image](https://user-images.githubusercontent.com/56099627/75567325-b1086b00-5a94-11ea-8358-78f8a8a34bd2.png)  
![image](https://user-images.githubusercontent.com/56099627/75567385-caa9b280-5a94-11ea-98c4-d7418abe2a5f.png)  
![image](https://user-images.githubusercontent.com/56099627/75567449-e614bd80-5a94-11ea-8e55-256baa5d6e93.png)  
-에러수정    
![image](https://user-images.githubusercontent.com/56099627/75607031-50316f00-5b36-11ea-9a28-455bfb0936b4.png)  
![image](https://user-images.githubusercontent.com/56099627/75607046-78b96900-5b36-11ea-9a65-e23e125b26a0.png)  
![image](https://user-images.githubusercontent.com/56099627/75607065-a7374400-5b36-11ea-8cb2-d48554189aca.png)  
![image](https://user-images.githubusercontent.com/56099627/75607083-c59d3f80-5b36-11ea-8329-e1fc145c1dbe.png)  
![image](https://user-images.githubusercontent.com/56099627/75607096-dbab0000-5b36-11ea-90b5-0908eeed7015.png)  
![image](https://user-images.githubusercontent.com/56099627/75607113-19a82400-5b37-11ea-8ce9-32cf776334f4.png) 
cuda 8.0에서 
$ pip install https://storage.googleapis.com/tensorflow/windows/gpu/tensorflow_gpu-1.4.0-cp36-cp36m-win_amd64.whl  
![image](https://user-images.githubusercontent.com/56099627/75607130-3f352d80-5b37-11ea-83c3-f76a69b3bb74.png)  
-참고사이트에 가서 찾아 다운로드하기 : opencv_python‑4.1.2+contrib‑cp36‑cp36m‑win_amd64.whl  
참고 사이트: https://www.lfd.uci.edu/~gohlke/pythonlibs/
![image](https://user-images.githubusercontent.com/56099627/75607138-5411c100-5b37-11ea-86ff-db8d69738560.png)  
![image](https://user-images.githubusercontent.com/56099627/75607150-6db30880-5b37-11ea-9be6-e097fc0da948.png)  

-에러발생: error: Unable to find vcvarsall.bat  
![image](https://user-images.githubusercontent.com/56099627/84219213-f5cb8580-ab0a-11ea-9d6f-fef146b280b0.png)  
--> (해결) visualcppbuildtools_full.exe 다운로드 받아서 설치해줬더니 잘 해결됨  
https://yellowtopaz.tistory.com/191  
--> 해결 후 인증  
![image](https://user-images.githubusercontent.com/56099627/84219520-b0f41e80-ab0b-11ea-8e10-634d25f202be.png)  

-에러수정  
![image](https://user-images.githubusercontent.com/56099627/75608132-29783600-5b40-11ea-8943-09a8eb2621cd.png)  
![image](https://user-images.githubusercontent.com/56099627/75610291-58e46e00-5b53-11ea-875f-01ddea8dd2fd.png)  
-> 해당 파일에 들어가서 주석 처리 했음  
![image](https://user-images.githubusercontent.com/56099627/75610306-79acc380-5b53-11ea-87ed-9106088d07c7.png)  
-> swig 설치 하고  
https://github.com/ildoonet/tf-pose-estimation/issues/554 을 참고하여 swig 설치하라  
http://blog.daum.net/purume77/7332107  을 참고하여 swig 설치하라  
-환경변수에 시스템환경변수PATH에 C:\Libs\swigwin-4.0.1 을 추가한다.(컴터를 다시켜기 하면 환경변수에 적용한거 활성화 될거임)  
![image](https://user-images.githubusercontent.com/56099627/84231624-81eca580-ab29-11ea-88d1-c6da442cc382.png)  

그런 후, 아래 그림처럼 설치  
1) $ swig -python -c++ pafprocess.i && python3 setup.py build_ext --inplace  
![image](https://user-images.githubusercontent.com/56099627/75610596-fd67af80-5b55-11ea-9076-3028e6b0db1d.png)  
![image](https://user-images.githubusercontent.com/56099627/75610622-2a1bc700-5b56-11ea-81da-8603e3cdc108.png)  
2) $ swig -python -c++ pafprocess.i && python3 setup.py build_ext --inplace  
![image](https://user-images.githubusercontent.com/56099627/84234088-87002380-ab2e-11ea-9c01-276f47dcc0f6.png)  

-추가 패키지 설치  
![image](https://user-images.githubusercontent.com/56099627/75611486-43c10c80-5b5e-11ea-9bc4-46846234b43f.png)  
![image](https://user-images.githubusercontent.com/56099627/75611520-7bc84f80-5b5e-11ea-8d27-64ce54c8c2e2.png)  
![image](https://user-images.githubusercontent.com/56099627/75611535-a4e8e000-5b5e-11ea-8f52-b2fa5f1392c9.png)  
![image](https://user-images.githubusercontent.com/56099627/75611540-c1851800-5b5e-11ea-89cd-d8f71ba348da.png)  
![image](https://user-images.githubusercontent.com/56099627/75611548-de215000-5b5e-11ea-9c78-1ea3e5accd28.png)  
![image](https://user-images.githubusercontent.com/56099627/75611570-00b36900-5b5f-11ea-9572-d659011e082e.png)  
![image](https://user-images.githubusercontent.com/56099627/75611586-22aceb80-5b5f-11ea-809d-4a4cd90d8fc1.png)  
![image](https://user-images.githubusercontent.com/56099627/75611600-3b1d0600-5b5f-11ea-8ce5-147aed98ffc5.png)  
-설치를 모두 다 했으니 이미지 넣고 결과를 보자!  
-명령여: python run.py --model=mobilenet_thin --resize=432x368 --image=./images/p1.jpg  
-근데 에러발생 : plt.show()을 할 수 없다.  
  -> install tkinter (python 용 GUI)
tkinter 참고자료:: https://light-tree.tistory.com/61  
![image](https://user-images.githubusercontent.com/56099627/75611844-80423780-5b61-11ea-9f6e-3b853a42f9fa.png)  
..중략..
![image](https://user-images.githubusercontent.com/56099627/75611861-9ea83300-5b61-11ea-9c1e-6460f40c8034.png)  
-명령어: python -c "import matplotlib; print(matplotlib.rcsetup.all_backends)"
-이 명령어로 matplotlib backend들을 조회할수 있다
![image](https://user-images.githubusercontent.com/56099627/75612159-59d1cb80-5b64-11ea-9d90-c83d1ff0e5ba.png)  
$ git clone https://github.com/cocodataset/cocoapi
$ cd cocoapi/PythonAPI
$ python3 setup.py build_ext --inplace
$ python3 setup.py build_ext install
참고사이트: https://github.com/ildoonet/tf-pose-estimation/blob/master/etcs/training.md
  
-train 할때 발생 하는 에러  
-First go to cocoapi\PythonAPI\setup.py and change line 14 from:  
extra_compile_args=['-Wno-cpp', '-Wno-unused-function', '-std=c99'],  
to  
extra_compile_args={'gcc': ['/Qstd=c99']},  
as pointed out in this issue: CharlesShang/FastMaskRCNN#173  
And then try to run make from cocoapi\PythonAPI\pycocotools again.  
참고사이트: https://github.com/cocodataset/cocoapi/issues/51  
![image](https://user-images.githubusercontent.com/56099627/75663702-9ca2b900-5cb4-11ea-9121-3343dea4f870.png)  
-수정후 train 명령어 build 결과(requirement.txt에서 pycocotools을 제외하고 셋팅된 가상환경)  
![image](https://user-images.githubusercontent.com/56099627/75663880-eb505300-5cb4-11ea-80a6-6326b78e7efc.png)  
![image](https://user-images.githubusercontent.com/56099627/75663977-16d33d80-5cb5-11ea-8fcd-de7460273659.png)  
![image](https://user-images.githubusercontent.com/56099627/75664156-59951580-5cb5-11ea-9b07-c279418d3eed.png)  
-수정후 train 명령어 build 결과(requirement.txt에서 pycocotools을 포함한 셋팅된 가상환경)  
![image](https://user-images.githubusercontent.com/56099627/75664381-bc86ac80-5cb5-11ea-97d1-d900b42b9b52.png)  
![image](https://user-images.githubusercontent.com/56099627/75664595-0b344680-5cb6-11ea-9f97-02debaf91cd3.png)  
-$ python3 setup.py build_ext --inplace
-$ python3 setup.py build_ext install
![image](https://user-images.githubusercontent.com/56099627/75665214-2a7fa380-5cb7-11ea-8139-acb3dfc6f1fd.png)  
![image](https://user-images.githubusercontent.com/56099627/75665256-3f5c3700-5cb7-11ea-9c72-501b0f3f33c4.png)  

-cocodataset 다운로드 하기  
-gustil 설치하기  
참고사이트: https://ukayzm.github.io/cocodataset/  
참고사이트: https://cloud.google.com/storage/docs/gsutil_install?hl=ko#windowsk%E3%85%8F  
![image](https://user-images.githubusercontent.com/56099627/75673703-e72d3100-5cc6-11ea-9d3c-54a9a9f972b4.png) 
![image](https://user-images.githubusercontent.com/56099627/75673872-4ab75e80-5cc7-11ea-9de8-5b7332b13722.png)  
![image](https://user-images.githubusercontent.com/56099627/75673955-79cdd000-5cc7-11ea-86a7-e650cdd2130b.png)
-gsutil 로 cocodataset 다운로드 에러나서 wget으로 다운로드 함  
참고사이트: https://gist.github.com/mkocabas/a6177fc00315403d31572e17700d7fd9  
![image](https://user-images.githubusercontent.com/56099627/75675063-b7335d00-5cc9-11ea-8471-9045cffdc54c.png)  
![image](https://user-images.githubusercontent.com/56099627/75675116-d631ef00-5cc9-11ea-8735-238d5f4825a7.png)  
-coco api 설치해야 coco annotation .json 파일 쉽게 확인 가능함
-cocodataset 다운로드 후에는 jq-win64.exe을 다운로드 하여 json파일에 들어있는 구성을 이쁘게 확인 할수 있다..
참고사이트: https://ukayzm.github.io/cocodataset/  
![image](https://user-images.githubusercontent.com/56099627/75784557-b53ecc00-5da5-11ea-9603-840d1eabbb9c.png)  
-coco api 빌드 후, pycocoDemo.ipynb 화면
![image](https://user-images.githubusercontent.com/56099627/75785107-90972400-5da6-11ea-8b9c-5521ca20cda6.png)  
