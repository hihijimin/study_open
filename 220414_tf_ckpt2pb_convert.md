참고 : https://gusrb.tistory.com/21  

## convert 시작하기
Converting the TensorFlow model checkpoint file.  .ckpt -> .pb  
일반적으로 tf 으로 학습하여 모델을 생성하면 .ckpt 파일로 생성된다  
생성된 체크포인트 파일로 바로 사용할 수 있으나,  
스크립트나 작업환경에 따라 다르지만 .pb 파일로 필요할 때가 있다. (protobuf)  
--> 이럴땐, 예제에서 제공한느 스크립트를 사용하면 된다! : freeze_graph.py  

## 시작
- freeze_graph.py 준비  
: https://github.com/tensorflow/tensorflow/blob/master/tensorflow/python/tools/freeze_graph.py  
- .ckpt 파일 준비 (학습 체크포인트 파일)  
![image](https://user-images.githubusercontent.com/56099627/163320985-3257f66c-6980-4f0c-99fc-3097402259d5.png)  
- .pbtxt 파일 준비 (그래프 정보)  
- tensorboardx 설치하여 텐서보드 설치해두기  
: 텐서보드 사용 (학습 시에) https://hyuna-tech.tistory.com/entry/Tensorboard-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EA%B0%84%EB%8B%A8%ED%95%9C-%EC%82%AC%EC%9A%A9%EB%B2%95-with-Pytorch 

- ckpt2pb
: https://github.com/r1cebank/tf-ckpt-2-pb
