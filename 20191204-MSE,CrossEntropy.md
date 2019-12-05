# 평균제곱오차(Mean Squared Error)
<img src="https://latex.codecogs.com/gif.latex?MSE=\frac{1}{n}\sum_{n}^{i=1}(y_{i}-t_{i})^{2}" title="MSE=\frac{1}{n}\sum_{n}^{i=1}(y_{i}-t_{i})^{2}" /> 
오차의 제곱에 대해 평균을 취한 것  
머신러닝 영역에선 cost function에서 주로 사용

# 교차 엔트로피 오차(Cross Entropy Error)
<img src="https://latex.codecogs.com/gif.latex?E=-\sum_{n}^{i=1}t_{k}log(y_{k})" title="E=-\sum_{n}^{i=1}t_{k}log(y_{k})" />  
yi : 예측한 값  
ti : 실제 정답 값   
i : 분류하고자 하는 class의 개수  

여기에서 yi, ti은 원핫인코딩 으로 되어 있음  
ti은 원핫인코딩에서 항상 1만 출력할거임 왜냐면 정답이니까  
그니까, ti(=1)X-log(x)를 하면 log(x)에 의해 좌우될 거임  
![image](https://user-images.githubusercontent.com/56099627/70142035-b9424b80-16db-11ea-8d91-9c6980aa0ca9.png)  
-log(x)는 위 그래프 처럼 생겼음  
(x=1 일 때<정답>, y=0) 그리고 (x=0 일 때<정답아님>, y=매우큰 무한대 양수)  
(x=0 일 때<정답아님>, y=매우큰 무한대 양수) 의 경우를 대비해서 yi에 1e-07 정도를 더해준다  
<div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div><div style="line-height:130%">3</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#a71d5d">def</span>&nbsp;cross_entropy_error(y,&nbsp;t):</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;delta&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>1e<span style="color:#0086b3"></span><span style="color:#a71d5d">-</span><span style="color:#0099cc">7</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#a71d5d">return</span>&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">-</span>np.sum(t<span style="color:#0086b3"></span><span style="color:#a71d5d">*</span>np.log(y<span style="color:#0086b3"></span><span style="color:#a71d5d">+</span>delta)</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>  


예측한 값(yi)이 
주의사항1: 교차엔트로피오차는 label 값이 one-hot-encording 일때만 사용이 가능하다.  
주의사항2: y와 log의 곱은 matrix 상에서 곱이 아닌 일반 곱셈에서 쓰임  






참고  
[1] 밑바닥 부터 시작하는 딥러닝, p114  
[2] https://worthpreading.tistory.com/23, Cross entropy error, CEE (교차 엔트로피 오차)  
