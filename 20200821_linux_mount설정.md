###
https://m.blog.naver.com/kimmingul/220639741333  
1. 먼저, sudo(관리자 권한)으로 fdisk -l 들어가 하드디스크(또는 ssd)가 잘 인식되는지 확인한다.  
인식이 잘 된다면 아래와 같이 (dvice 라고 표현 된건 마운트 된거) 표현된다 (/dev/sdb 3.7TB, /dev/sdd 3.7TB)  
![image](https://user-images.githubusercontent.com/56099627/90863952-cd91ba00-e3ca-11ea-9e01-39c03196c6e9.png)  
2. 
![image](https://user-images.githubusercontent.com/56099627/90863631-5825e980-e3ca-11ea-8302-51777e8625d0.png)  
3. $ sudo mkfs -t ext4 /dev/sda1
![image](https://user-images.githubusercontent.com/56099627/90863680-74c22180-e3ca-11ea-8148-448095a20633.png)
4. 새로운 하드디스크 사용 경로 설정 
- 여기에선 sudo 관리자 권한으로 해야함
```
원하는 경로에 설정 $ mkdir /home/사용자이름/data  
누구나 입출력할 수 있게 권한변경 $ sudo chmod 777 /home/사용자이름/data  
마운트 설정 $ sudo mount /dev/sda1 /home/사용자이름/data  
마운트! $ mount 
```
![image](https://user-images.githubusercontent.com/56099627/98892901-a5ef5100-24e4-11eb-81b7-696f34cfd6ae.png)  

### 2TB 이상 하드디스크 일때 마운트 방법
https://topis.me/109  
1. DOS 파티션으로는 2테라까지만 지원하니 GPT로 포맷하라는 안내가 메세지가 나오면 GPT으로 바꿔주면 된다  
![image](https://user-images.githubusercontent.com/56099627/90866268-9c1aed80-e3ce-11ea-878a-8d6069244fde.png)  
2. 확인(하지만 여전히 linux filesystem 이라고 되어 있을 것임 하지만 GPT으로 된게 맞음)  
![image](https://user-images.githubusercontent.com/56099627/90867799-e8ffc380-e3d0-11ea-874b-6867215537d5.png)  
3. 설정된 GPT 하드디스크를 포맷하기  
![image](https://user-images.githubusercontent.com/56099627/90867963-22d0ca00-e3d1-11ea-802a-b9e6ef592ad9.png)  


