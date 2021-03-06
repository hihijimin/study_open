# 객체추출 위한 DUC

`객체추출에 탁월한 DUC(Dense Upsampling Convolution) 알고리즘을 적용하였습니다. 이 알고리즘은 DeepLab-V2 ResNet-101 네트워크를 기본모델로 사용한 것으로 full-resolution label map을 한번에 처리 대신에 pixel-level accuracy map 단위로 처리하여 객체를 추출하는 방법입니다.` 
![image](https://user-images.githubusercontent.com/56099627/70226740-b6eff800-1794-11ea-934d-98b39efffc19.png)  
그림설명: ResNet-101 network with Hybrid Dilated Convolution (HDC)을 encording 하여 그림을 압축한 후, Dense Upsampling Convolution (DUC) layer(decording 과정) 거쳐 영상속 객체들을 인식한 결과를 도출한다.  
  
resnet101 은 feature extraction 하기 위한 과정
HDC은 3X3 연산량으로 5X5 영역까지 콘볼루션 할수 있는 방법.  
필터내부에 zero padding을 추가해 강제로 receptive field를 늘리는 방법이다. (센터 점과 양 끝점엔 값을 넣고 나머지엔 0으로 제로 패딩을 한다) receptive field란 필터가 한 번의 보는 영역으로 볼 수 있는데 사진의 전체적인 특징을 잡아내기 위해서는 이 receptive field가 높을 수록 좋다. 하지만 이 필터 크기를 크게하면 연산량이 늘어나고 오버피팅의 우려가 있다. 그래서 일반적으로 CNN에서는 이를 conv-pooling의 결합으로 해결한다. 즉, pooling을 통해 dimensiom을 줄이고 다시 작은 크기의 filter로 conv을 하면 전체적인 특징을 잡을 수 있다. 또 pooling을 하면 기존 정보의 손실이 일어난다 이를 해결하기 위해서 Dilated Convolution으로 pooling을 하지 않고도 receptive field의 크기를 크게 가져 가져갈수 있기 때문에 spatial dimension 의 손실이 적고 weight가 0이기 때문에 연산 효율도 좋다. 공간적 특징을 유지하는 특성 때문에 Dilated Convolution은 특히 segmentation에 많이 사용 된다.  
- (일반적인 방법)pooling-conv 이후, upsampling : 공간적인 손실 있음 - 업샘플링(디코딩) 하면 해상도 떨어짐  
- Dilated conv : receptive field을 크게 가져가면서 convolution을 하면 정보의 손실을 최대화 하고 해상도 좋음  
  
Dense upsampling conv 은 downdampling factor로 width, hight을 나눈다. d^2 개 만큼 feature map이 생성 된다(hXwX(d^2XL)). L은 클래스의 개수. 마지막에 이 feature map들을 H X W X L 으로 softmax layer을 사용하여 복원 시킨다.  
  
이 알고리즘의 핵심 아이디어는  
전체 label map을 feature map과 hight와 width가 동일한 동일한 d² 하위 파트로 나누는 것입니다.  
다시말해, 전체 레이블 맵을 여러개 채널의 작은 레이블 맵으로 변형 시키는 것  
  
**Upsampling (업샘플링의 역할을 좀더 자세히)**  
feature map level에서 segmentation 한 결과는 너무 coarse한 결과이다. 따라서, 이 coarse한 결과를 dense하게 (원래의 image size로) 만들어주어야 합니다. 그래서 upsampling을 사용한다. 그러면 각 class별로 dense한 segmentation 결과를 얻을 수 있다. 즉, 원래 image의 폭을 W, 높이를 H, 라고 한다면, WxHxL 의 dense heatmap결과를 얻을 수 있다.  
  
**Segmentation**  
그러나 우리는 결국 각 class 별 결과를 추정하고자 하는 것이 아니죠. 하나의 이미지에서 모든 class의 segmentation된 결과를 얻어야 한다. 그래서 윗 단계에서 얻어진 upsampling된 각 class별 heatmap을 softmax를 이용하여 가장 높은 확률을 가지는 class만 모아서 한장의 segmentation 이미지로 만든다.  
  
`보행 데이터를 입력으로 두고 출력 층에는 분류할 객체를 카테고리 별(사람, 건물, 배경 등)로 분류할 수 있도록 지정하였고 교차 엔트로피(Cross-Entropy) 형태의 오차 함수를 사용하여 출력층에서 활성화 함수의 도함수에 의한 영향을 제거하도록 하였습니다. 출력 맵에서 모든 픽셀 위치에 결과가 합계되며 SGD (Stochastic Gradient Descent)을 사용하여 결과를 최적화 시켜 최종적으로 객체를 카테고리별 분류를 할 수 있었습니다.`  
  
# skeleton 추출  
`vgg-19 네트워크는 3X3 의 비교적 작은 필터 크기를 사용하여 convolution 연산을 하는데 큰 필터로 한번 연산 하는 것보다 작은 필터로 여러번 연산하여 비선형성 처리가 수월하게 됩니다. 입력데이터가 10개 레이어 vgg-19 네트워크에 통과한 이미지 데이터는 feature가 강조된 형태로 출력됩니다. 출력된 데이터는 6개의 state의 입력으로 활용되어 affinity field 와 confidence map을 구하는데 이용하였습니다. 각 stage에서 정답 라벨과 feature 비교를 통해 loss을 구하고 이를 점점 줄여나가는 방향으로 최적화시켜 feature 들이 점점 사람의 관절 위치를 가리키게 하였습니다.`  
  
![image](https://user-images.githubusercontent.com/56099627/70232882-be1d0300-17a0-11ea-8674-48733f0b0de0.png)    
![image](https://user-images.githubusercontent.com/56099627/70232950-e1e04900-17a0-11ea-8720-65ec0ad068f2.png)  
  
목적은 RGB 이미지로 부터 사람의 body part에 대한 2D keypoint 를 구하는 것이다.  
vgg-19 네트워크의 앞 10개 레이어만 가지고 사용한다.  
10개 레이어 통과한 이미지는 feature가 강조된 형태로 output 출력한다.  
이 output은 stage 1~6을 거친다. affinity field와 confidence map 단계로 나뉜다.  
affinity field은 이미지속 2D keypoint가 누구것인지 파악하는데 쓰이고   
confidence map은 이이미속 2D keypoint 위치를 파악하는데 사용한다.  
  
**Confidence map (사람의 관절위치 파악)**  
우선 학습 초기단계에선 input 이미지에 따른 별 의미 없는 feature를 뽑게 된다. 하지만, 이 feature를 각 stage 마다human pose data와 비교를 하고, 그 차이점을 점점 줄여나가는 방향으로 optimize를 진행하게 되면 feature들은 점점 사람의 관절 위치를 가르키는 방향으로 나타나게 될 것이다.  
  
**Affinity field(각 관절 주인이 누구인가)**  
관절 주인이 누구인가를 파악하려면 각 part의 운동 방향에 대해 알 필요가 있다.  
affinity field 자체가 vector field이기 때문이다.(position 과 orientation)  
Confidence map을 추출할땐 각 joint에 heatmap을 1개씩 배정했기 때문에 16개의 joint가 검출되어 총 16+1 개의 heatmap을 추출한다면 Affinity field의 경우에는 서로 이어지는 2개의 joint마다 x방향 운동량, y방향 운동량을 지칭하는 vector field를 합산하여야 하기 때문에 각 confidence map에서 필요했던 heatmap의 갯수보다 2배 많은 34개의 heatmap이 필요하게 된다.  
개개인의 body part을 예측하기 위해 PAFs(part affinity fields)을 사용하여 사람의 body part간 연관도 학습 한다.  
  
confidence map과 affinity field를 조합하여 완성된 human skeleton 을 만든다. 조합할때는 greedy relaxation 을 통해 각 part를 조합하게 된다.  

## convolution 
![Alt Text](https://cdn-images-1.medium.com/max/1200/1*1okwhewf5KCtIPaFib4XaA.gif)
<p align="center"> 2D convolution using a kernel size of 3, stride of 1 and padding</p>
  
- 파란색이 input이며 초록색이 output입니다
- Kernel Size : kernel size는 convolution의 시야(view)를 결정합니다. 보통 2D에서 3x3 pixel로 사용합니다  
- Stride : stride는 이미지를 횡단할 때 커널의 스텝 사이즈를 결정합니다. 기본값은 1이지만 보통 Max Pooling과 비슷하게 이미지를 다운샘플링하기 위해 Stride를 2로 사용할 수 있습니다  
- Padding : Padding은 샘플 테두리를 어떻게 조절할지를 결정합니다. 패딩된 Convolution은 input과 동일한 output 차원을 유지하는 반면, 패딩되지 않은 Convolution은 커널이 1보다 큰 경우 테두리의 일부를 잘라버릴 수 있습니다
- Input & Output Channels : Convolution layer는 Input 채널의 특정 수(I)를 받아 output 채널의 특정 수(O)로 계산합니다. 이런 계층에서 필요한 파라미터의 수는 I*O*K로 계산할 수 있습니다. K는 커널의 수입니다  

## Dilated Convolutions (확장된 Convolution)
<img src="https://cdn-images-1.medium.com/max/1200/1*SVkgHoFoiMZkjy54zM_SUw.gif">
<p align="center"> 2D convolution using a 3 kernel with a dilation rate of 2 and no padding </p>
  
- Dilated Convolution은 Convolutional layer에 또 다른 파라미터인 dilation rate를 도입했습니다. dilation rate은 커널 사이의 간격을 정의합니다. dilation rate가 2인 3x3 커널은 9개의 파라미터를 사용하면서 5x5 커널과 동일한 시야(view)를 가집니다.
- 5x5 커널을 사용하고 두번째 열과 행을 모두 삭제하면 (3x3 커널을 사용한 경우 대비)동일한 계산 비용으로 더 넓은 시야를 제공합니다.
- Dilated convolution은 특히 real-time segmentation 분야에서 주로 사용됩니다. 넓은 시야가 필요하고 여러 convolution이나 큰 커널을 사용할 여유가 없는 경우 사용합니다
>> 역자 : Dilated Convolution은 필터 내부에 zero padding을 추가해 강제로 receptive field를 늘리는 방법입니다. 위 그림에서 진한 파란 부분만 weight가 있고 나머지 부분은 0으로 채워집니다. (receptive field : 필터가 한번 보는 영역으로 사진의 feature를 추출하기 위해선 receptive field가 높을수록 좋습니다)
pooling을 수행하지 않고도 receptive field를 크게 가져갈 수 있기 때문에 spatial dimension 손실이 적고 대부분의 weight가 0이기 때문에 연산의 효율이 좋습니다. 공간적 특징을 유지하기 때문에 Segmentation에서 많이 사용합니다

## Transposed Convolutions
(a.k.a. deconvolutions or fractionally strided convolutions)  
- Transposed Convolution은 deconvolutional layer와 동일한 공간 해상도를 생성하기 점은 유사하지만 실제 수행되는 수학 연산은 다릅니다.  Transposed Convolutional layer는 정기적인 convolution을 수행하며 공간의 변화를 되돌립니다.  
<img src="https://cdn-images-1.medium.com/max/1200/1*BMngs93_rm2_BpJFH2mS0Q.gif">
<p align="center"> 2D convolution with no padding, stride of 2 and kernel of 3</p>  
  
- 혼란스러울 수 있으므로 구체적인 예를 보겠습니다. convolution layer에 넣을 5x5 이미지가 있습니다. stride는 2, padding은 없고 kernel은 3x3입니다. 이 결과는 2x2 이미지가 생성됩니다.  
- 이 과정을 되돌리고 싶다면, 역 수학 연산을 위해 input의 각 픽셀으로부터 9개의 값을 뽑아야 합니다. 그 후에 우리는 stride가 2인 출력 이미지를 지나갑니다. 이 방법이 deconvolution입니다  
<img src="https://cdn-images-1.medium.com/max/1200/1*Lpn4nag_KRMfGkx1k6bV-g.gif">  
<p align="center"> Transposed 2D convolution with no padding, stride of 2 and kernel of 3 </p>  
<p align="center"> 인풋 데이터를 2칸 띄어 놓는것을 stride 2이고 filter가 곧 kernel 이므로 kernel 사이즈가 3 </p>  
  
- transposed convolution은 위와 같은 방법을 사용하지 않습니다. deconvolution과 공통점은 convolution 작업을 하면서 5x5 이미지의 output을 생성하는 것입니다. 이 작업을 하기 위해 input에 임의의 padding을 넣어야 합니다.  
- 상상할 수 있듯, 이 단계에선 위의 과정을 반대로 수행하지 않습니다.  
- 단순히 이전 공간 해상도를 재구성하고 convolution을 수행합니다. 수학적 역 관계는 아니지만 인코더-디코더 아키텍쳐의 경우 유용합니다. 이 방법은 2개의 별도 프로세스를 진행하는 것 대신 convolution된 이미지의 upscaling을 결합할 수 있습니다  



참고해서 보자  
[1] https://modulabs-biomedical.github.io/FCN, Fully Convolutional Networks for Semantic Segmentation  
[2] http://image-net.org/challenges/talks/2016/Multi-person%20pose%20estimation-CMU.pdf, openpose presentation slides  
[3] https://github.com/vdumoulin/conv_arithmetic, Convolution arithmetic, Convolution animations  
[4] https://m.blog.naver.com/PostView.nhn?blogId=worb1605&logNo=221266339261&proxyReferer=https%3A%2F%2Fwww.google.com%2F, Upsampling  
[5] https://zzsza.github.io/data/2018/06/25/upsampling-with-transposed-convolution/, Up-sampling with Transposed Convolution 번역
  
참고  
[1] Understanding Convolution for Semantic Segmentation, Panqu Wang  
[2] https://3months.tistory.com/213, Segmentation과 Dilated Convolution  
[3] https://medium.com/@sh.tsang/review-resnet-duc-hdc-dense-upsampling-convolution-and-hybrid-dilated-convolution-semantic-c4208227b1ca, Review: ResNet-DUC-HDC — Dense Upsampling Convolution and Hybrid Dilated Convolution (Semantic Segmentation)  
[4] https://m.blog.naver.com/PostView.nhn?blogId=worb1605&logNo=221297566317&proxyReferer=https%3A%2F%2Fwww.google.com%2F, Open Pose  
[5] http://blog.naver.com/PostView.nhn?blogId=kyy0810&logNo=221426685008&parentCategoryNo=&categoryNo=15&viewDate=&isShowPopularPosts=true&from=search, [c++/머신러닝] pose extimation : openpose review  
[6] Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields, Zhe Cao  
[7] https://modulabs-biomedical.github.io/FCN, Fully Convolutional Networks for Semantic Segmentation  
[8] https://zzsza.github.io/data/2018/02/23/introduction-convolution/, 딥러닝에서 사용되는 여러 유형의 Convolution 소개  
