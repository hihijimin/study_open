# Generalization
predcition functions에 training data을 수행했을 때 잘 작동하는 데 training data 외 데이터에서 작동하지 않을 수 있다. (overfitting)  
  
<p align="center"><img width="50%" src="https://user-images.githubusercontent.com/56099627/70882779-262adf00-2014-11ea-9828-10f77e1da1b1.png" /></p>  
  
# Regularization
- Regularization은 overfitting을 막기 위해 “simpler” prediction rules을 선호하도록 학습 알고리즘을 modifying 하는 행위  
- 학습 중인 weightn에 특정값으로 penalize 을 주기 위해 loss function을 modifying 하는 것을 말함  
  
### weight 를 정의하는 방법은?
<p align="center"><img width="50%" src="https://user-images.githubusercontent.com/56099627/70883267-c1708400-2015-11ea-8b99-673cd9971f02.png" /></p>  
- L2 norm of w (= Euclidean norm)  
- A norm is a measure of a vector’s length  
  
### Goal for minimization 
<img src="https://latex.codecogs.com/gif.latex?L(w)&plus;\lambda&space;\left&space;\|&space;w&space;\right&space;\|^{2}" title="L(w)+\lambda \left \| w \right \|^{2}" /></a>  
- L(w) 은 loss function  
- <img src="https://latex.codecogs.com/gif.latex?\lambda&space;\left&space;\|&space;w&space;\right&space;\|^{2}" title="\lambda \left \| w \right \|^{2}" /></a> 은 이것을 최소화 함으로써 w을 0에 가깝게 만드는 결과를 선호한다  
- 왜 squared을 사용해? square root을 제거 한다. 수학적으로 더 쉽게 작동하기 위해?  
- lambda 은 hyperparameter인데 low training loss 와 low weights 사이에 tradeoff 해서 잘 조절해야해  
  
<img src="https://latex.codecogs.com/gif.latex?L(w)&plus;\lambda&space;R(w)" title="L(w)+\lambda R(w)" /></a>  
- R(w)은 regularization term or regularizer or penalty 라고 불림  
- The squared L2 norm is one kind of penalty  
- lambda 은 **regularization strength** 라고 불림  
  
### L1, L2 Regularization
<img src="https://latex.codecogs.com/gif.latex?R(w)&space;=&space;||w||^{2}" title="R(w) = ||w||^{2}" /></a>  
- the most common type of regularization  
- linear regression 사용할 때, Ridge regression 이라고 불림  
- Logistic regression 사용할 때, L2가 default로 사용함  
- R(w)은 convex(볼록)한 성격? 가짐  
  
<img src="https://latex.codecogs.com/gif.latex?R(w)&space;=&space;||w||" title="R(w) = ||w||" /></a>   
- linear regression 사용할 때, Lasso 라고 불림  
- L1은 종종 weight 결과를 0으로 만들어주는데 반면 L2는 매우 작은 값으로 만들어 주지만 non-zero 임  
  
<img src="https://latex.codecogs.com/gif.latex?R(w)&space;=&space;\lambda&space;_{2}||w||_{2}^{2}&space;&plus;&space;\lambda&space;_{1}||w||_{1}" title="R(w) = \lambda _{2}||w||_{2}^{2} + \lambda _{1}||w||_{1}" /></a>  
- 두개를 합친 형태를 ElasticNet 이라 불림  
- 한가지 독립적으로 사용할 때보다 더 나은 weight 결과를 줌    
- 두 개의 pernalties 중에 더 중요한 것을 선택해서 hyperparameter을 조정 할 수 있음  
  
  
참고  
[1] https://cmci.colorado.edu/classes/INFO-4604/files/slides-6_regularization.pdf, Regularization, INFO-4604, Applied Machine Learning University of Colorado Boulder
