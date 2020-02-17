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
  
명령어 : **(alpapose) D:\AlphaPose> python setup.py build develop**  
![image](https://user-images.githubusercontent.com/56099627/74507535-0ba3b200-4f40-11ea-8046-23f1a23349d3.png)  
  
명령어 : **pip install http://download.pytorch.org/whl/cu90/torch-1.1.0-cp36-cp36m-win_amd64.whl**
![image](https://user-images.githubusercontent.com/56099627/74512015-aef9c480-4f4a-11ea-8daa-aa707ae37841.png)  


참고
https://gitmemory.com/Fang-Haoshu

        ./scripts/inference.sh ./configs/coco/hrnet/256x192_w32_lr1e-3.yaml ./pretrained_models/hrnet_w32_256x192.pth ./222.mp4
        ++ CONFIG=./configs/coco/hrnet/256x192_w32_lr1e-3.yaml
        ++ CKPT=./pretrained_models/hrnet_w32_256x192.pth
        ++ VIDEO=./222.mp4
        ++ OUTDIR=./examples/res
        ++ python scripts/demo_inference.py --cfg ./configs/coco/hrnet/256x192_w32_lr1e-3.yaml --checkpoint ./pretrained_models/hrnet_w32_256x192.pth --video ./222.mp4 --outdir ./examples/res --detector yolo --save_img --save_video
        Loading pose model from ./pretrained_models/hrnet_w32_256x192.pth...
        Loading YOLO model..
        Network successfully loaded
          0%|                                                                                                                                                                                     | 0/1510 [00:00<?, ?it/s]
        Could not find encoder for codec id 27: Encoder not found
        Try to use other video encoders...
        100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 1510/1510 [01:10<00:00, 21.44it/s]
        ===========================> Finish Model Running.
        ===========================> Rendering remaining images in the queue...
        ===========================> If this step takes too long, you can enable the --vis_fast flag to use fast rendering (real-time).
        Results have been written to json.
