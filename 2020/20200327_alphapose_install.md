alphapose github  
(global) https://github.com/MVIG-SJTU/AlphaPose  
(windows) https://github.com/MVIG-SJTU/AlphaPose/tree/pytorch  

create conda for AlphPose ~~
![image](https://user-images.githubusercontent.com/56099627/77866693-0cce3b80-726f-11ea-9097-6e11f35818c6.png)  
commend: conda install pytorch==1.1.0 torchvision==0.3.0
![image](https://user-images.githubusercontent.com/56099627/77866741-35563580-726f-11ea-8ba6-ff6385cbcf93.png)  

(Recommended) Install with conda  

    # 1. Create a conda virtual environment.
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


