

##  numba 으로 GPU 코드 실행
https://programmersought.com/article/29957543534/#21_llvm_55  
1. Check the relevant version information of Jetson : $ jetson_release -v  
2. numba 라이브러리 설치위해 ~!!  
2-1. install llvm  
```
- llvm10.0.0 download
$ wget https://github.com/llvm/llvm-project/releases/download/llvmorg-10.0.0/clang+llvm-10.0.0-aarch64-linux-gnu.tar.xz
- unzip
$ tar xJvf clang+llvm-10.0.0-aarch64-linux-gnu.tar.xz
- 환경 구성 수정
$ vim ~/.bashrc
export PATH=$PATH:/[clang+llvm-10.0.0-aarch64-linux-gnu 경로]/clang+llvm-10.0.0-aarch64-linux-gnu/bin
$ source ~/.bashrc
버전확인 $ clang++ -v 
```
2-2. install llvmlite  
![image](https://user-images.githubusercontent.com/56099627/123601919-2e7fef00-d833-11eb-905b-90d67e5d73c8.png)  

$ pip install llvmlite==0.34.0  

문제발생 : llvmlite==0.34.0 설치 중 cannot find -ltinfo && recipe for target 'libllvmlite.so' failed 에러발생 한다면?  
```
1）/usr/bin/ld: cannot find -ltinfo
2）Makefile.linux:20: recipe for target 'libllvmlite.so' failed
```
![image](https://user-images.githubusercontent.com/56099627/123602764-12c91880-d834-11eb-86c7-cecf3c9d5b13.png)  

**해결 :**  
해결 실행 문구1 : $ apt-cache search libtinfo  
```
# apt-cache search libtinfo 실행이 문제 없이 실행 된다면 아래 문구 나옴!
libtinfo-dev - developer's library for the low-level terminfo library
libtinfo5 - shared low-level terminfo library for terminal handling
libtinfo5-dbg - debugging/profiling library for the low-level terminfo library
```
해결 실행 문구2 : $ sudo apt-get install libtinfo-dev  
```
hihijimin@hihijimin-desktop:~/shl/clang+llvm-10.0.0-aarch64-linux-gnu/bin$ sudo apt-get install libtinfo-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  activity-log-manager archdetect-deb bamfdaemon bogl-bterm busybox-static compiz-core compiz-plugins-default
  cryptsetup-bin debhelper dh-autoreconf dh-strip-nondeterminism dpkg-repack gir1.2-accounts-1.0 gir1.2-gdata-0.0
  gir1.2-gst-plugins-base-1.0 gir1.2-gstreamer-1.0 gir1.2-harfbuzz-0.0 gir1.2-rb-3.0 gir1.2-signon-1.0
  gir1.2-timezonemap-1.0 gir1.2-totem-1.0 gir1.2-totemplparser-1.0 gir1.2-xkl-1.0 gnome-calculator gnome-system-monitor
  grub-common gtk3-nocsd icu-devtools kde-window-manager kpackagetool5 kwayland-data kwin-common kwin-x11
  libarchive-cpio-perl libatkmm-1.6-1v5 libboost-python1.65.1 libcairomm-1.0-1v5 libcolumbus1-common libcolumbus1v5
  libcompizconfig0 libdebian-installer4 libdecoration0 libdmapsharing-3.0-2 libegl1-mesa-dev libeigen3-dev
  libfile-stripnondeterminism-perl libgeonames-common libgeonames0 libgles2-mesa-dev libglibmm-2.4-1v5 libgpod-common
  libgpod4 libgraphite2-dev libgtk3-nocsd0 libgtkmm-3.0-1v5 libharfbuzz-gobject0 libicu-le-hb0 libiculx60
  libkdecorations2-5v5 libkdecorations2private5v5 libkf5activities5 libkf5declarative-data libkf5declarative5
  libkf5globalaccelprivate5 libkf5idletime5 libkf5kcmutils-data libkf5kcmutils5 libkf5package-data libkf5package5
  libkf5plasma5 libkf5quickaddons5 libkf5waylandclient5 libkf5waylandserver5 libkscreenlocker5 libkwin4-effect-builtins1
  libkwineffects11 libkwinglutils11 libkwinxrenderutils11 libmail-sendmail-perl libnm-gtk0 liborc-0.4-dev
  liborc-0.4-dev-bin libpanel-applet3 libpangomm-1.4-1v5 libpcre16-3 libpcre3-dev libpcre32-3 libpcrecpp0v5 libpinyin-data
  libpinyin13 libqt5designer5 libqt5help5 libqt5positioning5 libqt5sensors5 libqt5sql5 libqt5test5 libqt5webchannel5
  libqt5webkit5 libsgutils2-2 libsignon-glib1 libsys-hostname-long-perl libtimezonemap-data libtimezonemap1
  libunity-control-center1 libunity-core-6.0-9 libunity-misc4 libwayland-bin libwayland-dev libxcb-composite0
  libxcb-cursor0 libxcb-damage0 libxrandr-dev libxrender-dev libzeitgeist-1.0-1 os-prober pkg-config po-debconf
  qml-module-org-kde-kquickcontrolsaddons rdate session-shortcuts tasksel tasksel-data unity-asset-pool unity-greeter
  unity-lens-applications unity-lens-files unity-lens-music unity-lens-video unity-schemas unity-scope-video-remote
  unity-scopes-master-default unity-scopes-runner x11proto-randr-dev
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  libtinfo-dev
0 upgraded, 1 newly installed, 0 to remove and 5 not upgraded.
Need to get 74.2 kB of archives.
After this operation, 360 kB of additional disk space will be used.
Get:1 http://ports.ubuntu.com/ubuntu-ports bionic-updates/main arm64 libtinfo-dev arm64 6.1-1ubuntu1.18.04 [74.2 kB]
Fetched 74.2 kB in 2s (45.2 kB/s)       
Selecting previously unselected package libtinfo-dev:arm64.
(Reading database ... 164346 files and directories currently installed.)
Preparing to unpack .../libtinfo-dev_6.1-1ubuntu1.18.04_arm64.deb ...
Unpacking libtinfo-dev:arm64 (6.1-1ubuntu1.18.04) ...
Setting up libtinfo-dev:arm64 (6.1-1ubuntu1.18.04) ...
```
해결 실행 문구3 : apt-cache search libtinfo 와 sudo apt-get install libtinfo-dev 가 문제없이 잘 설치 되었다면, **$ pip install llvmlite==0.34.0** 다시 한번 설치!!  

2-3. install numba  
$ pip3 install numba  

문제 발생 : error "TBB version is too old, 2019 update 5, i.e. TBB_INTERFACE_VERSION >= 11005 required"  
![image](https://user-images.githubusercontent.com/56099627/123604150-891a4a80-d835-11eb-9035-c58474674485.png)  

**해결 :**  
```
아래 명령어를 하나씩 실행 한다. 빌드 실행 중간에 nano 꺼질 수 있음!  
$ git clone https://github.com/wjakob/tbb.git
$ cd tbb/build
$ cmake ..
$ make -j
$ sudo make install

그리고 이거 실행한다! 
$ sudo apt install libtbb-dev 
```
그리고 다시 한번 $ pip3 install numba  
```
# 아래와 같이 문구 나타나면 성공! 적인 numba 설치 완료!
hihijimin@hihijimin-desktop:~/shl/tbb/build$ pip install numba
Defaulting to user installation because normal site-packages is not writeable
Looking in indexes: https://pypi.tuna.tsinghua.edu.cn/simple
Collecting numba
  Downloading https://pypi.tuna.tsinghua.edu.cn/packages/5e/81/6fd1dd064bcf71a79da109e8966a39e2da61d68bf0bd1e0839fa997f8c41/numba-0.51.2.tar.gz (2.1 MB)
     |████████████████████████████████| 2.1 MB 708 kB/s 
Requirement already satisfied: llvmlite<0.35,>=0.34.0.dev0 in /home/zhihui/.local/lib/python3.6/site-packages (from numba) (0.34.0)
Requirement already satisfied: numpy>=1.15 in /usr/local/lib/python3.6/dist-packages (from numba) (1.16.1)
Requirement already satisfied: setuptools in /home/zhihui/.local/lib/python3.6/site-packages (from numba) (50.3.2)
Building wheels for collected packages: numba
  Building wheel for numba (setup.py) ... done
  Created wheel for numba: filename=numba-0.51.2-cp36-cp36m-linux_aarch64.whl size=2975288 sha256=494f4df1ba36fe4eb209827bead47b0910e35702eba0c39e5d83c8d0eb046e2b
  Stored in directory: /home/zhihui/.cache/pip/wheels/cc/7a/97/f45c63a61c0d48218e1f0091cac2adf05d5ff6ec5803cbc6ac
Successfully built numba
Installing collected packages: numba
Successfully installed numba-0.51.2
```

2-4. python 에 들어가서 numba 실행 해본다  

문제 발생 & 해결 : scipy >= 1.0 설치 요구!!한다면, **$ sudo pip3 install librosa** 실행  
($ sudo pip3 install librosa 이거 실행하면서, scipy >= 1.0 가 충족되게 설치된다!)  
https://learninone209186366.wordpress.com/2019/07/24/how-to-install-the-librosa-library-in-jetson-nano-or-aarch64-module/  
