- **텐서플로 설치 후, 확인해 보니 아래 내용과 같은 출력이 뜬다. futurewarning 같은게 잔뜩 뜨는데 해결방법은???**
  
------(에러내용)-------
>>> import tensorflow  
C:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\tensorflow\python\framework\dtypes.py:523: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint8 = np.dtype([("qint8", np.int8, 1)])  
C:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\tensorflow\python\framework\dtypes.py:524: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])  
C:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\tensorflow\python\framework\dtypes.py:525: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])  
C:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\tensorflow\python\framework\dtypes.py:524: FutureWarning: Passing (type, 1) or
 '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint8 = np.dtype([("quint8", np.uint8, 1)])  
C:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\tensorflow\python\framework\dtypes.py:525: FutureWarning: Passing (type, 1) or
 '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint16 = np.dtype([("qint16", np.int16, 1)])  
C:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\tensorflow\python\framework\dtypes.py:526: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])  
C:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\tensorflow\python\framework\dtypes.py:527: FutureWarning: Passing (type, 1) orC:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\tensorflow\python\framework\dtypes.py:526: FutureWarning: Passing (type, 1) or
 '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_quint16 = np.dtype([("quint16", np.uint16, 1)])  
C:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\tensorflow\python\framework\dtypes.py:527: FutureWarning: Passing (type, 1) or
 '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  _np_qint32 = np.dtype([("qint32", np.int32, 1)])  
C:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\tensorflow\python\framework\dtypes.py:532: FutureWarning: Passing (type, 1) or
 '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
  np_resource = np.dtype([("resource", np.ubyte, 1)])  
C:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\h5py\__init__.py:36: FutureWarning: Conversion of the second argument of issub
dtype from `float` to `np.floating` is deprecated. In future, it will be treated as `np.float64 == np.dtype(float).type`.
  from ._conv import register_converters as _register_converters  
  
### 해결방법
- Numpy 버전이 1.17 보다 낮아야합니다. 
  - (다음을 실행해보셔요 ~!) **pip install "numpy<1.17"** 작성

### 실행 후, 결과 인증 화면
![image](https://user-images.githubusercontent.com/56099627/71961031-ceaa1880-3239-11ea-8f1d-e9e0125727e5.png)  
- 더이상 futurewarning 이 뜨지 않음

  
참고
[1] https://okky.kr/article/610623, 텐서플로우를 사용하는데 출력하면 이상한게 잔뜩 뜹니다..
