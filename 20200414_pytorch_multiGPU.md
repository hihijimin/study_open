### PyTorch Data Parallel 기능 사용하기  
https://medium.com/daangn/pytorch-multi-gpu-%ED%95%99%EC%8A%B5-%EC%A0%9C%EB%8C%80%EB%A1%9C-%ED%95%98%EA%B8%B0-27270617936b  
### PyTorch 사용법 - 03. How to Use PyTorch
https://greeksharifa.github.io/pytorch/2018/11/10/pytorch-usage-03-How-to-Use-PyTorch/  
Pytorch LR(Learning Rate) Scheduler의 종류  
: LR(Learning Rate) Scheduler는 미리 지정한 횟수의 epoch이 지날 때마다 lr을 감소(decay)시켜준다. 이는 학습 초기에는 빠르게 학습을 진행시키다가 minimum 근처에 다다른 것 같으면 lr을 줄여서 더 최적점을 잘 찾아갈 수 있게 해주는 것이다.  

종류는 여러 개가 있는데, 마음에 드는 것을 선택하면 된다. 아래쪽에 어떻게 lr이 변화하는지 그림을 그려 놓았다.  

lr Scheduler의 종류:  
optim.lr_scheduler.LambdaLR: lambda 함수를 하나 받아 그 함수의 결과를 lr로 설정한다.  
optim.lr_scheduler.StepLR: 특정 step마다 lr을 gamma 비율만큼 감소시킨다.  
optim.lr_scheduler.MultiStepLR: StepLR과 비슷한데 매 step마다가 아닌 지정된 epoch에만 gamma 비율로 감소시킨다.  
optim.lr_scheduler.ExponentialLR: lr을 지수함수적으로 감소시킨다.  
optim.lr_scheduler.CosineAnnealingLR: lr을 cosine 함수의 형태처럼 변화시킨다. lr이 커졌다가 작아졌다가 한다.  
optim.lr_scheduler.ReduceLROnPlateau: 이 scheduler는 다른 것들과는 달리 학습이 잘 되고 있는지 아닌지에 따라 동적으로 lr을 변화시킬 수 있다. 보통 validation set의 loss를 인자로 주어서 사전에 지정한 epoch동안 loss가 줄어들지 않으면 lr을 감소시키는 방식이다.  

## Cornernet 관련 설명
https://jjeamin.github.io/paper/2019/10/22/cornernet/  
Q: what does pull loss and push loss mean??
- pull loss?  
the pull loss tries to make the distances of embeddings for top-left corner and bottom-right corner from the same object samll.  
- push loss?  
the push loss tries to make the distances of embeddings for top-left corners and bottom-right corners from different objects large.  
For more details, please refer to CornerNet.   
