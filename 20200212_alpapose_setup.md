# alphapose
alphapose github 사이트:  
https://github.com/MVIG-SJTU/AlphaPose/blob/master/docs/INSTALL.md  

# conda에 set up 하기 위한 절차
    # 1. Create a conda virtual environment. (가상환경 파기)
    conda create -n alphapose python=3.6 -y
    conda activate alphapose

    # 2. Install PyTorch 
    conda install pytorch==1.1.0 torchvision==0.3.0

    # 3. Get AlphaPose
    git clone https://github.com/MVIG-SJTU/AlphaPose.git
    cd AlphaPose

    # 4. install
    export PATH=/usr/local/cuda/bin/:$PATH
    export LD_LIBRARY_PATH=/usr/local/cuda/lib64/:$LD_LIBRARY_PATH
    pip install cython
    sudo apt-get install libyaml-dev
    python setup.py build develop

### Install PyTorch 
![image](https://user-images.githubusercontent.com/56099627/74317512-e5a2d400-4dbe-11ea-981f-dbf7ffa18a8f.png)  
참고한 사이트: https://pytorch.org/get-started/previous-versions/  

설치한 결과  
![image](https://user-images.githubusercontent.com/56099627/74317849-7679af80-4dbf-11ea-89a6-c0c45f175a2c.png)  
