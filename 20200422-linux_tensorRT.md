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
sudo pip3 install graphsurgeon-0.4.1-py2.py3-none-any.whl  
![image](https://user-images.githubusercontent.com/56099627/79959887-a8924680-84bf-11ea-80a9-d1237d0093c5.png)  

