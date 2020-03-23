$ rm -r -f filename  
: -r directory -f files All of delete  
$ sudo ln -s /usr/bin/python3 /usr/bin/python  
: link-file to copy newlink-newfile  
: 만약 target_dir이 이미 존재한다면 그 안에 새로운 링크를 만들게 된다.  

Numpy 버전이 1.17 보다 낮아야합니다.  
다음을 실행해보셔요 ~!  
pip install "numpy<1.17"  

텐서플로우 실행 오류 경고 해결 방법  
I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:1005] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero  
https://hiseon.me/data-analytics/tensorflow/tensorflow-numa-node-error/  
https://aciddust.github.io/blog/post/Tip-NUMA-node-read-from-SysFS-had-negative-value-1/  
![image](https://user-images.githubusercontent.com/56099627/77271174-59ef6200-6cf1-11ea-9b2c-04cf743bc04c.png)  
![image](https://user-images.githubusercontent.com/56099627/77271821-febe6f00-6cf2-11ea-84bc-7752e9f59ae9.png)  
