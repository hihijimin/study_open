# 구글 코랩에서 파일 다운로
from google.colab import drive  :'/content/gdrive' 이 경로는 '구글드라이브에 접속하겠다  
drive.mount('/content/gdrive')

-> 출력 결과
Go to this URL in a browser: https://accounts.google.com/o/oauth2/auth?client_id=947318989803-6bn6qk8qdgf4n4g3pfee6491hc0brc4i.apps.googleusercontent.com&redirect_uri=urn%3aietf%3awg%3aoauth%3a2.0%3aoob&response_type=code&scope=email%20https%3a%2f%2fwww.googleapis.com%2fauth%2fdocs.test%20https%3a%2f%2fwww.googleapis.com%2fauth%2fdrive%20https%3a%2f%2fwww.googleapis.com%2fauth%2fdrive.photos.readonly%20https%3a%2f%2fwww.googleapis.com%2fauth%2fpeopleapi.readonly  

Enter your authorization code:  
··········  (비번 입력 )
Mounted at /content/gdrive  

# 코랩 경로에 임의의 txt 파일을 만들어서 잘 되는지 테스트
with open('/content/gdrive/My Drive/foo.txt', 'w') as f:  
  f.write('Hello Google Drive!')  
  
잘 된다면 OK~!  
'/content/gdrive/My Drive/' 까지 필수 경로임!!  
