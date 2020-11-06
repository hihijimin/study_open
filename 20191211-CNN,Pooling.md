### CNN에 대한 설명이 자세한 블로그
http://taewan.kim/post/cnn/  

# CNN (Convolutional Neural Network)
**CNN 개발 역사??**  
초창기 CNN 개발한 분들이 고양이가 보는 것 마다 자극 받는 뇌의 위치가 다른것을 보고 아이디어를 얻어 CNN을 만들었다한다.  
즉, 'image 전체'를 보는 것이 아니라 '부분'을 보는 것이 핵심 아이디어 이다.  
'부분'에 해당하는 것이 **filter** 이다.
  
![image](https://user-images.githubusercontent.com/56099627/70595067-a2dd4800-1c25-11ea-95ce-b22d760e35bf.png)  
7x7 이미지에 3x3 filter (stride=1) 으로 옆으로 옮겨가며 1개의 value을 얻게 된다.  
k= (7-3)/1 +1 =5 (N=7, F=3, stride=1)  
이 과정을 반복하면 총 5x5의 output(convolution layer)을 얻게 된다.  
  
**계산 (1개의 filter로 부터 얻는 convolution layer)**  
- image size : N (N x N)   
- filter size : F (F x F)  
- output size : K =(N-F) /stride +1  
  
**filter 하나당 activation 하나 주어지면 1개의 convolution layer 얻는다.**  
예를들어 6개의 filter로 부터 6개의 activation 거쳐 최종적으로 6개의 convolution layer을 얻었다면 N=7, F=3 으므로 5x5짜리 convolution layer을 6개 얻은 셈이다. 그러므로 5x5x6 인 convolution layers (다른말로 activation maps 라 부름)  
이렇게 convolution layers (activation maps) 까지 얻는 일련의 과정을 **convolution** 이라고 한다.  
(convolution 마다 쓰이는 weight은 다른 딥러닝 기법들과 마찬가지로 학습을 통해 얻을 수 있다. Relu 같은 activation func 사용하여)  
  
# convolution에서 padding을 왜 하는지 보면?
convolution 하는 자체가 수학적으로 차원이 낮아지는 것을 의미한다. 왜냐면 7x7 data가 convolution을 거쳐 5x5 data가 되므로~~  
49차원으로 표현되는 data가 25차원으로 확~~ 떨어지는 것이므로 (일반적으로 convolution 을 거치기 전부터 25차원 data에 embedding 되어 있지 않기 때문에) 데이터 손실은 불가피 할 것이다   
**그래서 convolution을 하고도 7x7의 형태를 그대로 유지하면 데이터 손실을 피할수 있지 않느냐 그 방법은 zero padding 이라는 technique 사용한다**  
아래, 위, 양 옆을 0으로 덧댐(padding =1)으로서 9x9으로 확장한다. 확장된 9x9 이미지에 convolution을 하면 7x7 짜리 convolution layer을 얻게 되고 원래 이미지와 같은 사이즈의 convolution layer을 얻어 데이터 손실을 막을 수 있게 된다.  **단점은 필요없는 부분이 생기는 것, 즉 노이즈가 발생하게 된다. 하지만 padding 없을때 데이터 손실과 padding 있을때 노이즈 생성을 비교했을 때 노이즈 생성 되었을 때가 더 나으니까 쓰는 거, 그나마 nosie가 주는 오류를 최소화 하기 위해 **
  
 **계산 (1개의 filter로 부터 얻는 convolution layer)**  
- image size : N (N x N)   
- filter size : F (F x F) conv 레이어의 receptive field size   
- Padding size : p  
- output size : K =( (N+2p) -F) /stride +1   
  
# pooling 을 왜 하는건지?
**김성훈 교수님 강의** 에서는 Pooling을 다음과 같이 정의한다.  
- convolution을 거쳐 나온 actication maps 가 있을 때, 이를 이루는 convolution layer을 **resizing** 하여 새로운 layer을 얻는 것  
- pooling을 하는 이유는 **overfitting을 방지** 하기 위함

**pooling의 종류**  
max pooling : 최댓값을 뽑아내는 것  
maen pooling : 평균값을 뽑아내는 것  
  
stride =2 이면서 2x2 filter을 통해 max pooling을 한다면  
![image](https://user-images.githubusercontent.com/56099627/70594289-5e50ad00-1c23-11ea-85f5-a2eca11423ac.png)  
각 pixel 마다 최대값(평균값도 이런식으로 하면 됌)을 뽑아낸다
  
  
참고  
[1] https://mc.ai/cnn%EC%97%90%EC%84%9C-pooling%EC%9D%B4%EB%9E%80/, CNN에서 pooling이란?  
[2] https://medium.com/@hobinjeong/cnn-convolutional-neural-network-9f600dd3b395, CNN(Convolutional Neural Network)이란?
