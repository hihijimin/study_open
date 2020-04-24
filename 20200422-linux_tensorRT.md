## tensorrt 설치하기 
참고 사이트:  
https://github.com/tkwoo/archive/wiki/TensorRT  
먼저, cuda 10.0 해당하는 tensorrt 다운로드 하기  
https://developer.nvidia.com/tensorrt    
TensorRT-5.1.5.0 (CUDA 10.0)  
![image](https://user-images.githubusercontent.com/56099627/79955493-d83e5000-84b9-11ea-9b99-4c2a1d1c0513.png)  

    2. tar 파일 압축 해제
    $ tar xzvf TensorRT-5.1.x.x.Ubuntu-1x.04.x.x86_64-gnu.cuda-x.x.cudnn7.x.tar.gz

    3. LD_LIBRARY_PATH 추가하기 
    $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:<eg:TensorRT-5.1.x.x/lib>

    4. 휠 파일 설치 
    python 2.7 or python 3.x 버전에 따라 pip2 or pip3 사용하여 설치 

    $ cd TensorRT-5.1.x.x/python
      # for python 2.7
    $ sudo pip2 install tensorrt-5.1.x.x-cp27-none-linux_x86_64.whl
      # for python 3.x
    $ sudo pip3 install tensorrt-5.1.x.x-cp3x-none-linux_x86_64.whl

    $ cd TensorRT-5.1.x.x/uff
      # for python 2.7
    $ sudo pip2 install uff-0.6.3-py2.py3-none-any.whl
      # for python 3.x
    $ sudo pip3 install uff-0.6.3-py2.py3-none-any.whl

    # 위치 /usr/local/bin/convert-to-uff 인지 확인
    $ which convert-to-uff

    $ cd TensorRT-5.1.x.x/graphsurgeon
      # for python 2.7
    $ sudo pip2 install graphsurgeon-0.4.0-py2.py3-none-any.whl
      # for python 3.x
    $ sudo pip3 install graphsurgeon-0.4.0-py2.py3-none-any.whl

    5. 설치 확인 
    $ tree-d
    $ python
      import tensorrt as trt
      
$ cd TensorRT-5.1.x.x/python (for python 3.6)  
$ sudo pip3 install tensorrt-5.1.5.0-cp36-none-linux_x86_64.whl  
![image](https://user-images.githubusercontent.com/56099627/79957639-d629c080-84bc-11ea-8e66-e46977cf7d35.png)  
$ cd TensorRT-5.1.x.x/uff (for python 3.6)  
$ sudo pip3 install uff-0.6.3-py2.py3-none-any.whl  
![image](https://user-images.githubusercontent.com/56099627/79958257-adee9180-84bd-11ea-8f20-0ab71fee377d.png)  
$ which convert-to-uff  
![image](https://user-images.githubusercontent.com/56099627/79959801-84366a00-84bf-11ea-8538-5a99d3ea8d84.png)  
$ sudo pip3 install graphsurgeon-0.4.1-py2.py3-none-any.whl  
![image](https://user-images.githubusercontent.com/56099627/79959887-a8924680-84bf-11ea-80a9-d1237d0093c5.png)  
tensorrt 설치된 cuda&tensorrt 패키지 보기  
$ dpkg -l | grep TensorRT  
![image](https://user-images.githubusercontent.com/56099627/80086576-df865c00-8594-11ea-822b-0aa1d860433f.png)  
  
tensorrt sample_mnist 실행해보기  
![image](https://user-images.githubusercontent.com/56099627/79963785-c910cf80-84c4-11ea-8b91-80d052a70b3d.png)  

import tensorflow.contrib.tensorrt

tensorrt 설치 전 pycuda 설치해야함  
https://docs.nvidia.com/deeplearning/sdk/tensorrt-install-guide/index.html  
위 사이트에 들어가 보면 pycuda 설치하라고 나와있음 (아래 내용 증거)  
2. Getting Started  
Ensure you are familiar with the following installation requirements and notes.  
The Windows zip package for TensorRT does not provide Python support. Python may be supported in the future.
**If you are using the TensorRT Python API and PyCUDA isn’t already installed on your system, see Installing PyCUDA. If you encounter any issues with PyCUDA usage, you may need to recompile it yourself. For more information, see Installing PyCUDA on Linux.**  
pycuda 설치는 링크(**Installing PyCUDA on Linux.**) 따라가보면 https://wiki.tiker.net/PyCuda/Installation/Linux 여기 사이트가 나옴 
여기 사이트 순서대로 설치해주면 됌  

다운로드 파일: tar xzvf pycuda-2019.1.2.tar.gz  
다운로드 파일 사이트: https://pypi.org/project/pycuda/#files  
![image](https://user-images.githubusercontent.com/56099627/79968729-80104980-84cb-11ea-802a-5eb15b53a2ff.png)  
내꺼 쿠다 경로: CUDA_HOME=/usr/local/cuda-10.0  
python configure.py --cuda-root=/usr/local/cuda-10.0  
  
$ cd pycuda-VERSION # if you're not there already  
$ python configure.py --cuda-root=/usr/local/cuda-10.0  
$ su -c "make install"  
Step 4: Test PyCUDA  
![image](https://user-images.githubusercontent.com/56099627/79969037-e7c69480-84cb-11ea-84d8-594f8d9a06f5.png)  



