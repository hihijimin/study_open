## 기본 도커 환경 이미지 다운로드 하기
도커허브 사이트 -> 검색: 1.7.0-cuda11.0-cudnn8 환경에 pytorch 설치된 이미지 (예 : pytorch/pytorch:$1.7.0-cuda11.1-cudnn7-devel)  

## 
도커 실행 후, 필수 라이브러리 설치하기 
opencv 설치 하기 위한 ~ 참고: https://webnautes.tistory.com/1186
```
# OpenCV 컴파일 전 필요한 패키지 설치
apt-get update && apt-get upgrade -y
apt-get install gcc g++
apt-get install git
apt-get install build-essential cmake
apt-get install pkg-config
apt-get install libjpeg-dev libtiff5-dev libpng-dev
apt-get install libavcodec-dev libavformat-dev libswscale-dev libxvidcore-dev libx264-dev libxine2-dev
apt-get install libv4l-dev v4l-utils
apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev 
apt-get install libgtk2.0-dev
apt-get install mesa-utils libgl1-mesa-dri libgtkgl2.0-dev libgtkglext1-dev
apt-get install libatlas-base-dev gfortran libeigen3-dev  
apt-get install python2.7-dev python3-dev python-numpy python3-numpy

# opencv 깃으로 설치 <4.1.0 버전>
# opencv
git clone https://github.com/opencv/opencv.git
cd opencv
git checkout 4.1.0
cd .. #get out of opencv folder
# opencv_contrib
git clone https://github.com/opencv/opencv_contrib/
cd opencv_contrib
git checkout 4.1.0
cd .. #get out of opencv_contrib folder
# opencv 폴더 안에 빌듣 디렉토리 만들고 opencv_contrib를 참조
cd opencv
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=RELEASE -D OPENCV_ENABLE_NONFREE=ON -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules -D WITH_GTK=ON ..
make
sudo make install
```
