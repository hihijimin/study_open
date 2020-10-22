1. 설치  
설치는 아래 설치 링크에서 첫 두 줄까지만 (서버는 이미 만들어져 있음)  
설치: https://dejavuqa.tistory.com/12?category=266924  
$ sudo apt-get install subversion  
$ sudo svnadmin create /home/svn/nglerepo  

2. 체크아웃: local 에 svn 파일 가져오기  
체크아웃: https://dejavuqa.tistory.com/124?category=266924  
$ svn checkout --username [username] --password [password] svn://000.000.0.00/svn  
3. 커밋 (file 경로는 체크아웃하여 local에 svn 저장된 위치에 커밋할 파일이 있어야함)  
커밋: https://dejavuqa.tistory.com/145?category=266924  
$ svn add svn_test (실제 파일은 .txt 이지만 .txt은 생략해서~)  
$ svn commit [filename]   
![image](https://user-images.githubusercontent.com/56099627/96854650-b472bb80-1496-11eb-9271-d4412e479813.png)  
![image](https://user-images.githubusercontent.com/56099627/96854364-5c3bb980-1496-11eb-84b0-2ca2b38cbb06.png)  
```
* 환경설정 참고: 
svn commit [filename] 할때 .bashrc에 환경설정해 줘야만 vim 으로 실행 한다
export SVN_EDITOR=vim 
```
추가 참고: https://kutar37.tistory.com/entry/%EC%9E%90%EC%A3%BC-%EC%93%B0%EC%9D%B4%EB%8A%94-SVN-Commands-10-%EC%98%88%EC%A0%9C  
