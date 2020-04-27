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

## ModuleNotFoundError: No module named 'tensorrt'
http://www.bojankomazec.com/2019/12/how-to-install-tensorrt-python-package.html  
    Source code of the following Python script contains:  

    import tensorrt as trt

    ...and its execution fails:


    (tensorflow-demo) nvidia@nvidia-nano:~/dev/nvidia/uff_ssd$ python detect_objects.py images/image1.jpg
    Traceback (most recent call last):
      File "detect_objects.py", line 58, in <module>
        import tensorrt as trt
    ModuleNotFoundError: No module named 'tensorrt'

    TensorRT Pyton module was not installed. I want to share here my experience with the process of setting up TensorRT on Jetson Nano as described here:
    A Guide to using TensorRT on the Nvidia Jetson Nano - Donkey Car

    $ sudo find / -name nvcc
    [sudo] password for nvidia:
    find: ‘/run/user/1000/gvfs’: Permission denied
    find: ‘/run/user/120/gvfs’: Permission denied
    /usr/local/cuda-10.0/bin/nvcc
    /home/nvidia/.cache/bazel/_bazel_nvidia/0c75cc683915a1db7f4f8a4da90fb148/execroot/org_tensorflow/bazel-out/host/bin/external/local_config_cuda/cuda/cuda/bin/nvcc
    /home/nvidia/.cache/bazel/_bazel_nvidia/0c75cc683915a1db7f4f8a4da90fb148/execroot/org_tensorflow/bazel-out/aarch64-py2-opt/bin/external/local_config_cuda/cuda/cuda/bin/nvcc
    /home/nvidia/.cache/bazel/_bazel_nvidia/0c75cc683915a1db7f4f8a4da90fb148/execroot/org_tensorflow/bazel-out/aarch64-opt/bin/external/local_config_cuda/cuda/cuda/bin/nvcc


    nvidia@nvidia-nano:/usr/src/tensorrt/samples/python$ /usr/local/cuda-10.0/bin/nvcc --version
    nvcc: NVIDIA (R) Cuda compiler driver
    Copyright (c) 2005-2019 NVIDIA Corporation
    Built on Mon_Mar_11_22:13:24_CDT_2019
    Cuda compilation tools, release 10.0, V10.0.326


    nvidia@nvidia-nano:/usr/src/tensorrt/samples/python$ cd /usr/local/cuda

    nvidia@nvidia-nano:/usr/local/cuda$ ls
    bin  extras   lib64    NsightCompute-1.0  nvvm    samples  targets  version.txt
    doc  include  LICENSE  nvml               README  share    tools

    nvidia@nvidia-nano:/usr/local/cuda$ cd bin

    nvidia@nvidia-nano:/usr/local/cuda/bin$ ls
    bin2c     cuda-gdbserver                fatbinary     nvlink
    crt       cuda-install-samples-10.0.sh  nvcc          nvprof
    cudafe++  cuda-memcheck                 nvcc.profile  nvprune
    cuda-gdb  cuobjdump                     nvdisasm      ptxas

    nvidia@nvidia-nano:/usr/local/cuda/bin$ ls -la
    total 57272
    drwxr-xr-x  3 root root     4096 Aug 16 19:42 .
    drwxr-xr-x 12 root root     4096 Aug 16 19:43 ..
    -rwxr-xr-x  1 root root    60600 Mar 12  2019 bin2c
    drwxr-xr-x  2 root root     4096 Aug 16 19:36 crt
    -rwxr-xr-x  1 root root  3960000 Mar 12  2019 cudafe++
    -rwxr-xr-x  1 root root  6143896 Mar 12  2019 cuda-gdb
    -rwxr-xr-x  1 root root   472429 Mar 12  2019 cuda-gdbserver
    -rwxr-xr-x  1 root root      784 Mar 12  2019 cuda-install-samples-10.0.sh
    -rwxr-xr-x  1 root root   259368 Mar 12  2019 cuda-memcheck
    -rwxr-xr-x  1 root root   270128 Mar 12  2019 cuobjdump
    -rwxr-xr-x  1 root root   119280 Mar 12  2019 fatbinary
    -rwxr-xr-x  1 root root   180816 Mar 12  2019 nvcc
    -rw-r--r--  1 root root      393 Mar 12  2019 nvcc.profile
    -rwxr-xr-x  1 root root 22607128 Mar 12  2019 nvdisasm
    -rwxr-xr-x  1 root root  8979096 Mar 12  2019 nvlink
    -rwxr-xr-x  1 root root  6597104 Mar 12  2019 nvprof
    -rwxr-xr-x  1 root root    77280 Mar 12  2019 nvprune
    -rwxr-xr-x  1 root root  8874104 Mar 12  2019 ptxas

    nvidia@nvidia-nano:/usr/local/cuda/bin$ ./nvcc --version
    nvcc: NVIDIA (R) Cuda compiler driver
    Copyright (c) 2005-2019 NVIDIA Corporation
    Built on Mon_Mar_11_22:13:24_CDT_2019
    Cuda compilation tools, release 10.0, V10.0.326

    nvidia@nvidia-nano:/usr/src/tensorrt/samples/python$ sudo gedit ~/.bashrc

    # Add this to your .bashrc file
    export CUDA_HOME=/usr/local/cuda
    # Adds the CUDA compiler to the PATH
    export PATH=$CUDA_HOME/bin:$PATH
    # Adds the libraries
    export LD_LIBRARY_PATH=$CUDA_HOME/lib64:$LD_LIBRARY_PATH

    nvidia@nvidia-nano:/usr/src/tensorrt/samples/python$ source ~/.bashrc

    nvidia@nvidia-nano:/usr/src/tensorrt/samples/python$ nvcc --version
    nvcc: NVIDIA (R) Cuda compiler driver
    Copyright (c) 2005-2019 NVIDIA Corporation
    Built on Mon_Mar_11_22:13:24_CDT_2019
    Cuda compilation tools, release 10.0, V10.0.326

    Just after I issued pip install pycuda:

    nvidia@nvidia-nano:~$ sudo find / -name *pycuda*
    [sudo] password for nvidia: 
    find: ‘/run/user/1000/gvfs’: Permission denied
    find: ‘/run/user/120/gvfs’: Permission denied
    /tmp/pip-install-sf96wq0d/pycuda
    /tmp/pip-install-sf96wq0d/pycuda/pycuda.egg-info
    /tmp/pip-install-sf96wq0d/pycuda/build/lib.linux-aarch64-3.6/pycuda
    /tmp/pip-install-sf96wq0d/pycuda/build/lib.linux-aarch64-3.6/pycuda/cuda/pycuda-helpers.hpp
    /tmp/pip-install-sf96wq0d/pycuda/build/lib.linux-aarch64-3.6/pycuda/cuda/pycuda-complex.hpp
    /tmp/pip-install-sf96wq0d/pycuda/build/lib.linux-aarch64-3.6/pycuda/cuda/pycuda-complex-impl.hpp
    /tmp/pip-install-sf96wq0d/pycuda/pycuda
    /tmp/pip-install-sf96wq0d/pycuda/pycuda/cuda/pycuda-helpers.hpp
    /tmp/pip-install-sf96wq0d/pycuda/pycuda/cuda/pycuda-complex.hpp
    /tmp/pip-install-sf96wq0d/pycuda/pycuda/cuda/pycuda-complex-impl.hpp
    /tmp/pip-install-sf96wq0d/pycuda/pip-egg-info/pycuda.egg-info
    /tmp/pip-install-sf96wq0d/pycuda/bpl-subset/bpl_subset/pycudaboost

    Installing pycuda:

    (tensorflow-demo) nvidia@nvidia-nano:/usr/src/tensorrt/samples/python$ pip install pycuda
    Collecting pycuda
      Using cached https://files.pythonhosted.org/packages/5e/3f/5658c38579b41866ba21ee1b5020b8225cec86fe717e4b1c5c972de0a33c/pycuda-2019.1.2.tar.gz
    Requirement already satisfied: pytools>=2011.2 in /home/nvidia/python-envs/tensorflow-demo/lib/python3.6/site-packages (from pycuda) (2019.1.1)
    Requirement already satisfied: decorator>=3.2.0 in /home/nvidia/python-envs/tensorflow-demo/lib/python3.6/site-packages (from pycuda) (4.4.1)
    Requirement already satisfied: appdirs>=1.4.0 in /home/nvidia/python-envs/tensorflow-demo/lib/python3.6/site-packages (from pycuda) (1.4.3)
    Requirement already satisfied: mako in /home/nvidia/python-envs/tensorflow-demo/lib/python3.6/site-packages (from pycuda) (1.1.0)
    Requirement already satisfied: six>=1.8.0 in /home/nvidia/python-envs/tensorflow-demo/lib/python3.6/site-packages (from pytools>=2011.2->pycuda) (1.13.0)
    Requirement already satisfied: numpy>=1.6.0 in /home/nvidia/python-envs/tensorflow-demo/lib/python3.6/site-packages (from pytools>=2011.2->pycuda) (1.17.4)
    Requirement already satisfied: MarkupSafe>=0.9.2 in /home/nvidia/python-envs/tensorflow-demo/lib/python3.6/site-packages (from mako->pycuda) (1.1.1)
    Building wheels for collected packages: pycuda
      Building wheel for pycuda (setup.py) ... done
      Created wheel for pycuda: filename=pycuda-2019.1.2-cp36-cp36m-linux_aarch64.whl size=4497309 sha256=e7bbecd3bfa86a84f2ed505966a51123d97073cb4fd981ed434959f20a7507f3
      Stored in directory: /home/nvidia/.cache/pip/wheels/a6/60/f0/b1c430c73d281ac3e46070480db50f7907364eb6f6d3188396
    Successfully built pycuda
    Installing collected packages: pycuda
    Successfully installed pycuda-2019.1.2

    Let's see where is now pycuda:

    nvidia@nvidia-nano:~$ sudo find / -name *pycuda*
    find: ‘/run/user/1000/gvfs’: Permission denied
    find: ‘/run/user/120/gvfs’: Permission denied
    /home/nvidia/.cache/pip/wheels/a6/60/f0/b1c430c73d281ac3e46070480db50f7907364eb6f6d3188396/pycuda-2019.1.2-cp36-cp36m-linux_aarch64.whl
    /home/nvidia/python-envs/tensorflow-demo/lib/python3.6/site-packages/pycuda-2019.1.2.dist-info
    /home/nvidia/python-envs/tensorflow-demo/lib/python3.6/site-packages/pycuda
    /home/nvidia/python-envs/tensorflow-demo/lib/python3.6/site-packages/pycuda/cuda/pycuda-helpers.hpp
    /home/nvidia/python-envs/tensorflow-demo/lib/python3.6/site-packages/pycuda/cuda/pycuda-complex.hpp
    /home/nvidia/python-envs/tensorflow-demo/lib/python3.6/site-packages/pycuda/cuda/pycuda-complex-impl.hpp

    Let's find TensorRT:

    nvidia@nvidia-nano:~$ ls -la /usr/lib/python3.6/dist-packages
    total 4272
    drwxrwxr-x 10 root root    4096 Nov 28 22:43 .
    drwxr-xr-x 33 root root   20480 Dec  7 23:46 ..
    -rw-r--r--  1 root root 2831864 Feb  6  2019 cv2.cpython-36m-aarch64-linux-gnu.so
    drwxr-xr-x  2 root root    4096 Aug 16 19:52 graphsurgeon
    drwxr-xr-x  2 root root    4096 Aug 16 19:52 graphsurgeon-0.4.1.dist-info
    drwxr-xr-x  4 root root    4096 Nov 28 22:43 jetson
    drwxr-xr-x  4 root root    4096 Nov 28 22:43 Jetson
    -rw-r--r--  1 root root  746496 Nov 28 22:43 jetson_inference_python.so
    -rw-r--r--  1 root root  725512 Nov 28 22:43 jetson_utils_python.so
    drwxr-xr-x  3 root root    4096 Aug 16 19:52 tensorrt
    drwxr-xr-x  2 root root    4096 Aug 16 19:52 tensorrt-5.1.6.1.dist-info
    drwxr-xr-x  5 root root    4096 Aug 16 19:52 uff
    drwxr-xr-x  2 root root    4096 Aug 16 19:52 uff-0.6.3.dist-info

    nvidia@nvidia-nano:~$ ls -la /usr/lib/python3.6/dist-packages/tensorrt
    total 2156
    drwxr-xr-x  3 root root    4096 Aug 16 19:52 .
    drwxrwxr-x 10 root root    4096 Nov 28 22:43 ..
    -rw-r--r--  1 root root    2914 Jun  4  2019 __init__.py
    drwxr-xr-x  6 root root    4096 Aug 16 19:52 legacy
    -rw-r--r--  1 root root 2190376 Jun  4  2019 tensorrt.so


    TensorRT is still not visible to Python in virtual environment though:

    (tensorflow-demo) nvidia@nvidia-nano:/usr/src/tensorrt/samples/python$ python -c "import tensorrt as trt"
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
    ModuleNotFoundError: No module named 'tensorrt'

    We need to add the path to TensorRT package to PYTHONPATH in virtual environment:

    (tensorflow-demo) nvidia@nvidia-nano:/usr/src/tensorrt/samples/python$ export PYTHONPATH=/usr/lib/python3.6/dist-packages:$PYTHONPATH

    TensorRT is now visible to Python:

    (tensorflow-demo) nvidia@nvidia-nano:/usr/src/tensorrt/samples/python$ python -c "import tensorrt as trt"

    (tensorflow-demo) nvidia@nvidia-nano:/usr/src/tensorrt/samples/python$ python
    Python 3.6.9 (default, Nov  7 2019, 10:44:02) 
    [GCC 8.3.0] on linux
    Type "help", "copyright", "credits" or "license" for more information.
    >>> import tensorrt as trt
    >>> trt.__version__
    '5.1.6.1'
    >>> 

