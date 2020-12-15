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
5. 영구 마운트  
- UUID 확인: $ sudo blkid  
https://kilim.tistory.com/155
- UUID 확인한 정보를 등록해주기  
$ sudo vim /etc/fstab  
![image](https://user-images.githubusercontent.com/56099627/98916663-c6cc9c00-250e-11eb-8466-fb9e8429919b.png)  
![image](https://user-images.githubusercontent.com/56099627/101147751-1f9bda00-3660-11eb-91e9-06de1e094e2a.png)  
- reboot 하기  

### 2TB 이상 하드디스크 일때 마운트 방법
https://topis.me/109  
1. DOS 파티션으로는 2테라까지만 지원하니 GPT로 포맷하라는 안내가 메세지가 나오면 GPT으로 바꿔주면 된다  
![image](https://user-images.githubusercontent.com/56099627/90866268-9c1aed80-e3ce-11ea-878a-8d6069244fde.png)  
2. 확인(하지만 여전히 linux filesystem 이라고 되어 있을 것임 하지만 GPT으로 된게 맞음)  
![image](https://user-images.githubusercontent.com/56099627/90867799-e8ffc380-e3d0-11ea-874b-6867215537d5.png)  
3. 설정된 GPT 하드디스크를 포맷하기  
![image](https://user-images.githubusercontent.com/56099627/90867963-22d0ca00-e3d1-11ea-802a-b9e6ef592ad9.png)  

### 2TB 이상 하드디스크 마운트 할때 발생한 에러
https://m.blog.naver.com/PostView.nhn?blogId=rbar&logNo=220569935459&proxyReferer=https:%2F%2Fwww.google.com%2F  
```
The disk contains an unclean file system (0, 0).
Metadata kept in Windows cache, refused to mount.
Falling back to read-only mount because the NTFS partition is in an
unsafe state. Please resume and shutdown Windows fully (no hibernation
or fast restarting.)
```
- 일단 터미널에서 마운트 명령을 내려본다
```
jimin@jimin-System:~$ sudo mount /dev/sda1 /home/jimin/HDD2
The disk contains an unclean file system (0, 0).
Metadata kept in Windows cache, refused to mount.
Falling back to read-only mount because the NTFS partition is in an
unsafe state. Please resume and shutdown Windows fully (no hibernation
or fast restarting.)
```
- 주절 주절 NTFS 파티션이 문제가 있다는 오류 메시지가 뜨면 ntfsfix 명령으로 해결한다
$ sudo ntfsfix /dev/sda1  
```
jimin@jimin-System:~$ sudo ntfsfix /dev/sda1
Mounting volume... The disk contains an unclean file system (0, 0).
Metadata kept in Windows cache, refused to mount.
FAILED
Attempting to correct errors... 
Processing $MFT and $MFTMirr...
Reading $MFT... OK
Reading $MFTMirr... OK
Comparing $MFTMirr to $MFT... OK
Processing of $MFT and $MFTMirr completed successfully.
Setting required flags on partition... OK
Going to empty the journal ($LogFile)... OK
Checking the alternate boot sector... OK
NTFS volume version is 3.1.
NTFS partition /dev/sda1 was processed successfully.
```
