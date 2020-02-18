참고 1  
https://tobeagoodmom.tistory.com/2174  
- 1. 가상환경 만들어주고 (파이썬 환경 셋업)
  - 명령어 **(base) C:\Users\humanict>conda create --name caffe_dev**
  - 가상환경 활성화 **(base) C:\Users\humanict>conda activate caffe_dev**
- 2. opencv 셋업  
  - **(caffe_dev) C:\Users\humanict>conda install opencv=4.2.0**
- 3. 라이브러리 셋업
  - **(caffe_dev) C:\Users\humanict>conda install scikit-image**  
- 4. CUDA 설치 되어 있다면 패스
- 5. caffe 셋업
# caffe 셋업
git clone https://github.com/BVLC/caffe.git  
cd caffe  
cp Makefile.config.example Makefile.config (해당 폴더-파일 들어가서 수정하기!)  

    < 아나콘다 파이썬을 사용한다면 **주석 처리** 하기 >
    Makefile.config 파일에서 두가지만 체크!
    CPU_ONLY := 1
    PYTHON_INCLUDE := /usr/local/include/python2.7 \
                                              /usr/local/include/python2.7/numpy

    < 아나콘다 파이썬을 사용한다면 **주석 해제** 하기 >
    ANACONDA_HOME := $(HOME)/anaconda 
    PYTHON_INCLUDE := $(ANACONDA_HOME)/include \ 
      # $(ANACONDA_HOME)/include/python2.7 \ 
      # $(ANACONDA_HOME)/lib/python2.7/dist-packages/numpy/core/include \

    # We need to be able to find libpythonX.X.so or .dylib. 
    # PYTHON_LIB := /usr/lib PYTHON_LIB := $(ANACONDA_HOME)/lib


