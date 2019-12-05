# Wavelet Trasform/ Furier Transform/ Principle component Analysis
신호는 다양한 주파수와 크기를 가진 사인 곡선들의 합해서 표현할수 있다
여러개의 사인 곡선으로 분해한 다음에 그 곡선들이 어떤 주파수들로 존재하는지 알아낼 수 있다.  
  
**푸리에 변환** 은 신호내에 존재하는 주파수들을 분석할 수 있는 장점이 있지만 시간에 대한 정보가 사라진다  
그래서 각 주파수가 시간적으로 언제 존재하는지 알 수 없다는 한계가 있다.
예를 들면 20초의 10hz, 20hz 주파수 성분을 갖는 신호가 있다고 가정하면 푸리에 변환으로 10, 20 hz의 성분의 신호가 있다고는 알 수 있지만 10hz신호와 20hz 신호를 구분해 낼수 없다.
음의 높이(주파수)에 따라 배열되어 있기 때문에 그렇다.
다시말해, 주파수 성분들은 알 수 있지만 주파수 성분이 어느 구간에 배치되어 있는지 알수 없다.
  
푸리에 변환 사용하는 이유: 시간영역에서 해석하기 곤란한 신호의 주파수 성분과 진폭등을 쉽게 파악할 수 있다.
![image](https://user-images.githubusercontent.com/56099627/70221852-6aa0ba00-178c-11ea-9f20-6fe10629aace.png)
식설명: 푸리에 변환 
![image](https://user-images.githubusercontent.com/56099627/70222085-cb2ff700-178c-11ea-987e-45a8b3445f1a.png)  
식설명: 역푸리에 변환  
  
**단시간 푸리에 변환(STFT)**  
푸리에변환의 한계를 돌파하기 위해 제안된 방법
시간에 따라 변화하는 긴 신호를 짧은 시간 단위로 분할한 다음에 푸리에 변환을 적용하는 것이다.
짧은 시간 단위로 분할 할 수록 어떤 시간에 어떤 주파수가 존재하는지 알기 쉬워진다.
즉, 윈도우(window) 사이즈가 작을 수록 분해능이 좋아진다.
그러나, 주파수 분해능과 시간분해능이 동시에 좋아지는 것은 불가능하다.
나름대로 적절한 지점을 찾아야 한다.

**웨이블릿 변환(WT)**  
단시간 푸리에 변환의 한계를 극복하기 위해 제안된 방법  
시간 해상도에 따라 주파수 해상도를 달리하는 방법  
시간 해상도를 높이고 주파수 해상도를 낮춘다.  
  
![image](https://user-images.githubusercontent.com/56099627/70218330-28747a00-1786-11ea-9df7-a6571766be0c.png)  
그림설명: (왼) 짧은 시간 단위으로 STFT는 분해능 좋다, (중) 긴 시간 단위 신호으로 STFT는 분해능이 안좋다, (오) 저주파수 성분엔 긴 시간 단위 트랜스폼, 고주파 성분엔 짧은 시간 단위 트랜스폼 WT  
  
시간적으로 무한한 사인곡선을 기본함수로 사용하는 푸리에 변환과는 달리 웨이블릿 변환은 시간적으로 한정되어 있다.
웨이블릿 변환은 여러종류 있다. 
  
![image](https://user-images.githubusercontent.com/56099627/70220293-b30aa880-1789-11ea-9d58-ef4ed1b726a6.png)  
그림설명: 다양한 웨이블릿 형태들
  
위 그림에서 웨이블릿 형태 한가지를 선택한 후, 그 선택한 웨이블릿을 가져와 원래 신호와 비교한다. 비교한 결과 상관계수가 나온다(아래 그림 참고) 그리고 옆으로 이동해서 마찬가지로 웨이블릿과 해당 구간 신호와 비교하고 상관계수를 얻는다. 신호가 끝날때가지 반복한다. 끝나면 신호 
![image](https://user-images.githubusercontent.com/56099627/70220576-290f0f80-178a-11ea-84bb-8edd2d055d71.png)  
그림설명: 웨이블릿 변환 절차 




참고  
[1] https://bskyvision.com/404, 푸리에 변환과 웨이블릿 변환 비교  
[2] https://www.mathworks.com/videos/understanding-wavelets-part-1-what-are-wavelets-121279.html, (그림출처)  
[3] https://slideplayer.com/slide/7537671/, Lecture 13 Wavelet transformation II. Fourier Transform (FT) Forward FT: Inverse FT: Examples: + + + Slide from Alexander Kolesnikov ’s lecture notes.(그림출처)  
