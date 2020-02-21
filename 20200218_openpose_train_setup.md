참고 1  
https://tobeagoodmom.tistory.com/2174  
1\. 가상환경 만들어주고 (파이썬 환경 셋업)
  - 명령어 **(base) C:\Users\humanict>conda create --name caffe_dev**
  - 가상환경 활성화 **(base) C:\Users\humanict>conda activate caffe_dev**
2\. opencv 셋업  
  - **(caffe_dev) C:\Users\humanict>conda install opencv=4.2.0**
3\. 라이브러리 셋업
  - **(caffe_dev) C:\Users\humanict>conda install scikit-image**  
4\. CUDA 설치 되어 있다면 패스
5\. caffe 셋업
# caffe 셋업
### caffe 셋업 성공 케이스
- 참고1: caffe-window 다운로드  
https://github.com/happynear/caffe-windows/tree/ms/windows  
https://github.com/happynear/caffe-windows  
- 참고2: third party library 다운로드  
https://drive.google.com/file/d/13dbvXmMosxozWbSgJdDdxH62YWqXLjoJ/view  
- 참고3: 설명 잘된 블로그
https://bearhouse0923.tistory.com/4  
  
1\. 참고1 (https://github.com/happynear/caffe-windo) 여기에서 caffe-window 다운로드 할것  
2\. 위 참고2에서 thrid party library 다운로드 후, 압축 해제 한 후, caffe-window -> windows -> thridparty에 내용을 복사할 것
![image](https://user-images.githubusercontent.com/56099627/74998404-fd074e80-549b-11ea-85f4-ce1705547713.png)  
3\. caffe-window -> windows 폴더에서 **CommonSetting.prop.example**을 복사하여 **CommonSetting.prop**이라고 만들것  
4\. CommonSetting.prop 내용 변경(바꿔 줘야 할게 은근 많음)  

5\. caffe.sln(프로젝트) 빌드  
libcaffe -> caffe -> caffe.binding -> pycaffe 순서로 빌드 진행  
파이썬에서만 사용할 경우 release에서만 빌드 하면 됨  
  빌드 환경은 release - x64 이고, 
  <<--- MY CommonSettings 수정된 내용 --->>  
  
    <CpuOnlyBuild>true</CpuOnlyBuild>  
    <UseCuDNN>false</UseCuDNN>  
    <UseNCCL>true</UseNCCL>  
    <UseMKL>false</UseMKL>  
    <CudaVersion>9.0</CudaVersion>  
    <CudaArchitecture>compute_52,sm_52;compute_60,sm_60;</CudaArchitecture>  
    <CuDnnPath>C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\</CuDnnPath>  
    <PythonDir>C:\Users\humanict\Anaconda36</PythonDir>  
     <ItemDefinitionGroup Condition="'$(CpuOnlyBuild)'=='true'">  
    <ItemDefinitionGroup Condition="'$(UseCuDNN)'=='true'">  
    <ItemDefinitionGroup Condition="'$(UseNCCL)'=='flase'">  
  
    <?xml version="1.0" encoding="utf-8"?>
    <Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <ImportGroup Label="PropertySheets" />
      <PropertyGroup Label="UserMacros">
        <BuildDir>$(SolutionDir)..\Build</BuildDir>
        <!--NOTE: CpuOnlyBuild and UseCuDNN flags can't be set at the same time.-->
        <CpuOnlyBuild>true</CpuOnlyBuild>
        <UseCuDNN>false</UseCuDNN>
        <UseNCCL>true</UseNCCL>
        <UseMKL>false</UseMKL>
        <CudaVersion>9.0</CudaVersion>
        <!-- NOTE: If Python support is enabled, PythonDir (below) needs to be
             set to the root of your Python installation. If your Python installation
             does not contain debug libraries, debug build will not work. -->
        <PythonSupport>true</PythonSupport>

        <!-- NOTE: If Matlab support is enabled, MatlabDir (below) needs to be
             set to the root of your Matlab installation. -->
        <MatlabSupport>true</MatlabSupport>
        <MXNetSupport>true</MXNetSupport>
        <CudaDependencies>cufft.lib</CudaDependencies>
        <BoostIncludeFolder>$(SolutionDir)thirdparty\Boost</BoostIncludeFolder>
        <BoostLibraryFolder>$(SolutionDir)thirdparty\Boost\lib64-msvc-14.0</BoostLibraryFolder>
        <HDF5Root>$(SolutionDir)thirdparty\HDF5</HDF5Root>
        <GFlagsRoot>$(SolutionDir)thirdparty\GFlags</GFlagsRoot>
        <GLogRoot>$(SolutionDir)thirdparty\Glog</GLogRoot>
        <ProtobufRoot>$(SolutionDir)thirdparty\Protobuf</ProtobufRoot>
        <ProtocDir>$(ProtobufRoot)\bin\</ProtocDir>
        <OpenCVRoot>$(SolutionDir)thirdparty\OpenCV</OpenCVRoot>
        <LMDBRoot>$(SolutionDir)thirdparty\LMDB</LMDBRoot>
        <OpenBLASRoot>$(SolutionDir)thirdparty\OpenBLAS</OpenBLASRoot>
        <LevelDBRoot>$(SolutionDir)thirdparty\LEVELDB</LevelDBRoot>
        <NCCLRoot>$(SolutionDir)thirdparty\NCCL</NCCLRoot>
        <MKLRoot>D:\ThirdPartyLibrary\IntelSWTools\compilers_and_libraries_2017.4.210\windows\mkl</MKLRoot>
        <MXNetRoot>D:\deepLearning\mxnet</MXNetRoot>

        <!-- Set CUDA architecture suitable for your GPU.
             Setting proper architecture is important to mimize your run and compile time. -->
        <CudaArchitecture>compute_52,sm_52;compute_60,sm_60;</CudaArchitecture>

        <!-- CuDNN 3 and 4 are supported -->
        <CuDnnPath>C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\</CuDnnPath>
        <ScriptsDir>$(SolutionDir)\scripts</ScriptsDir>
      </PropertyGroup>
      <PropertyGroup Condition="'$(CpuOnlyBuild)'=='false'">
        <CudaDependencies>cublas.lib;cuda.lib;curand.lib;cudart.lib</CudaDependencies>
      </PropertyGroup>

      <PropertyGroup Condition="'$(UseCuDNN)'=='true'">
        <CudaDependencies>cudnn.lib;$(CudaDependencies)</CudaDependencies>
      </PropertyGroup>
      <PropertyGroup Condition="'$(UseCuDNN)'=='true' And $(CuDnnPath)!=''">
        <LibraryPath>$(CuDnnPath)\lib\x64;$(LibraryPath)</LibraryPath>
        <IncludePath>$(CuDnnPath)\include;$(IncludePath)</IncludePath>
      </PropertyGroup>

      <PropertyGroup Condition="'$(UseNCCL)'=='true' And $(NCCLRoot)!=''">
        <CudaDependencies>nccl.lib;$(CudaDependencies)</CudaDependencies>
        <LibraryPath>$(NCCLRoot)\lib;$(LibraryPath)</LibraryPath>
        <IncludePath>$(NCCLRoot)\include;$(IncludePath)</IncludePath>
      </PropertyGroup>
      <PropertyGroup Condition="'$(UseMKL)'=='true' And $(MKLRoot)!=''">
        <LibraryPath>$(MKLRoot)\lib\intel64_win;$(LibraryPath)</LibraryPath>
        <IncludePath>$(MKLRoot)\include;$(IncludePath)</IncludePath>
        <AdditionalDependencies>mkl_rt.lib;$(AdditionalDependencies)</AdditionalDependencies>
      </PropertyGroup>
      <PropertyGroup Condition="'$(UseMKL)'=='false' Or $(MKLRoot)==''">
        <LibraryPath>$(OpenBLASRoot)\lib;$(LibraryPath)</LibraryPath>
        <IncludePath>$(OpenBLASRoot)\include;$(IncludePath)</IncludePath>
        <AdditionalDependencies>libopenblas.dll.a;$(AdditionalDependencies)</AdditionalDependencies>
      </PropertyGroup>

      <PropertyGroup>
        <OutDir>$(BuildDir)\$(Platform)\$(Configuration)\</OutDir>
        <IntDir>$(BuildDir)\Int\$(ProjectName)\$(Platform)\$(Configuration)\</IntDir>
      </PropertyGroup>
      <PropertyGroup>
        <LibraryPath>$(OutDir);$(CUDA_PATH)\lib\$(Platform);$(BoostLibraryFolder);$(HDF5Root)\lib;$(GFlagsRoot)\lib;$(GLogRoot)\lib;$(ProtobufRoot)\lib;$(OpenCVRoot)\x64\vc14\lib;$(LMDBRoot)\lib;$(LevelDBRoot)\lib;$(LibraryPath)</LibraryPath>
        <IncludePath>$(SolutionDir)..\include;$(SolutionDir)..\include\caffe\proto;$(CUDA_PATH)\include;$(BoostIncludeFolder);$(HDF5Root)\include;$(GFlagsRoot)\include;$(GLogRoot)\include;$(ProtobufRoot)\include;$(OpenCVRoot)\include;$(LMDBRoot)\include;$(LevelDBRoot)\include;$(IncludePath)</IncludePath>
      </PropertyGroup>
      <PropertyGroup Condition="'$(PythonSupport)'=='true'">
        <PythonDir>C:\Users\humanict\Anaconda36</PythonDir>
        <LibraryPath>$(PythonDir)\libs;$(LibraryPath)</LibraryPath>
        <IncludePath>$(PythonDir)\include;$(IncludePath)</IncludePath>
      </PropertyGroup>
      <PropertyGroup Condition="'$(MatlabSupport)'=='true'">
        <MatlabDir>C:\Program Files\MATLAB\R2016a</MatlabDir>
        <LibraryPath>$(MatlabDir)\extern\lib\win64\microsoft;$(LibraryPath)</LibraryPath>
        <IncludePath>$(MatlabDir)\extern\include;$(IncludePath)</IncludePath>
      </PropertyGroup>
      <ItemDefinitionGroup Condition="'$(CpuOnlyBuild)'=='true'">
        <ClCompile>
          <PreprocessorDefinitions>CPU_ONLY;%(PreprocessorDefinitions)</PreprocessorDefinitions>
        </ClCompile>
      </ItemDefinitionGroup>
      <ItemDefinitionGroup Condition="'$(UseCuDNN)'=='true'">
        <ClCompile>
          <PreprocessorDefinitions>USE_CUDNN;%(PreprocessorDefinitions)</PreprocessorDefinitions>
        </ClCompile>
        <CudaCompile>
          <Defines>USE_CUDNN</Defines>
        </CudaCompile>
      </ItemDefinitionGroup>
      <ItemDefinitionGroup Condition="'$(UseNCCL)'=='flase'">
        <ClCompile>
          <PreprocessorDefinitions>USE_NCCL;%(PreprocessorDefinitions)</PreprocessorDefinitions>
        </ClCompile>
        <CudaCompile>
          <Defines>USE_NCCL</Defines>
        </CudaCompile>
      </ItemDefinitionGroup>
      <ItemDefinitionGroup Condition="'$(UseMKL)'=='true'">
        <ClCompile>
          <PreprocessorDefinitions>USE_MKL;%(PreprocessorDefinitions)</PreprocessorDefinitions>
        </ClCompile>
        <CudaCompile>
          <Defines>USE_MKL</Defines>
        </CudaCompile>
      </ItemDefinitionGroup>
      <ItemDefinitionGroup Condition="'$(PythonSupport)'=='true'">
        <ClCompile>
          <PreprocessorDefinitions>WITH_PYTHON_LAYER;BOOST_PYTHON_STATIC_LIB;%(PreprocessorDefinitions)</PreprocessorDefinitions>
        </ClCompile>
      </ItemDefinitionGroup>
      <ItemDefinitionGroup Condition="'$(MatlabSupport)'=='true'">
        <ClCompile>
          <PreprocessorDefinitions>MATLAB_MEX_FILE;%(PreprocessorDefinitions)</PreprocessorDefinitions>
        </ClCompile>
      </ItemDefinitionGroup>
      <ItemDefinitionGroup>
        <ClCompile>
          <MinimalRebuild>false</MinimalRebuild>
          <MultiProcessorCompilation>true</MultiProcessorCompilation>
          <PreprocessorDefinitions>_SCL_SECURE_NO_WARNINGS;USE_OPENCV;USE_LEVELDB;USE_LMDB;%(PreprocessorDefinitions)</PreprocessorDefinitions>
          <TreatWarningAsError>false</TreatWarningAsError>
        </ClCompile>
      </ItemDefinitionGroup>
      <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Release|x64'">
        <ClCompile>
          <Optimization>Full</Optimization>
          <PreprocessorDefinitions>NDEBUG;%(PreprocessorDefinitions)</PreprocessorDefinitions>
          <RuntimeLibrary>MultiThreadedDLL</RuntimeLibrary>
          <FunctionLevelLinking>true</FunctionLevelLinking>
          <DisableSpecificWarnings>4819;</DisableSpecificWarnings>
        </ClCompile>
        <Link>
          <EnableCOMDATFolding>true</EnableCOMDATFolding>
          <GenerateDebugInformation>true</GenerateDebugInformation>
          <LinkTimeCodeGeneration>UseLinkTimeCodeGeneration</LinkTimeCodeGeneration>
          <OptimizeReferences>true</OptimizeReferences>
          <AdditionalDependencies>leveldb.lib;Advapi32.lib;Shlwapi.lib;lmdb.lib;opencv_world310.lib;libprotobuf.lib;glog.lib;gflags.lib;hdf5_tools.lib;hdf5_hl_fortran.lib;hdf5_fortran.lib;hdf5_hl_f90cstub.lib;hdf5_f90cstub.lib;hdf5_cpp.lib;hdf5_hl_cpp.lib;hdf5_hl.lib;hdf5.lib;zlib.lib;szip.lib;$(AdditionalDependencies)</AdditionalDependencies>
        </Link>
      </ItemDefinitionGroup>
      <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Debug|x64'">
        <ClCompile>
          <Optimization>Disabled</Optimization>
          <PreprocessorDefinitions>_DEBUG;%(PreprocessorDefinitions)</PreprocessorDefinitions>
          <RuntimeLibrary>MultiThreadedDebugDLL</RuntimeLibrary>
          <DisableSpecificWarnings>4819;</DisableSpecificWarnings>
        </ClCompile>
        <Link>
          <GenerateDebugInformation>true</GenerateDebugInformation>
          <AdditionalDependencies>leveldbd.lib;Advapi32.lib;Shlwapi.lib;lmdbd.lib;opencv_world310d.lib;libprotobufd.lib;glogd.lib;gflagsd.lib;hdf5_tools.lib;hdf5_hl_fortran.lib;hdf5_fortran.lib;hdf5_hl_f90cstub.lib;hdf5_f90cstub.lib;hdf5_cpp.lib;hdf5_hl_cpp.lib;hdf5_hl.lib;hdf5.lib;zlib.lib;szip.lib;$(AdditionalDependencies)</AdditionalDependencies>
        </Link>
      </ItemDefinitionGroup>
    </Project>  

6/. 각 빌드 후, 발생한 에러는 인터넷 서치하면서 해결 !
7/. 빌드(컴파일) **끝나면 C:\Library\caffe-windows\caffe-windows\Build\x64\Release\pycaffe 가 생성된다.  
여기 안의 caffe 폴더를 통채로 C:\Anaconda3\lib\site-package 안에 복사한다**  
8/. python에서 caffe 사용하기 위한 환경 설정  
  빌드한 pycaffe 폴더를 환경 변수 내 PYTHONPATH 에 새로 추가한다  
  그런 후, python에서 import caffe 해서 테스트 해본다  
  테스트 예시 : python -c "import caffe; print(caffe.__version__)"  

-------------------------------------------------------
### caffe 셋업 잘 안된 케이스
- 참고1: 설치하는 방법 매우 자세히 잘 나와있음!!
https://baemincheon.tistory.com/21  
- 참고2: 에러에 대처하는 방법 자세히 나와 있음(중국어)!!
https://www.geek-share.com/detail/2748721992.html  
  
![image](https://user-images.githubusercontent.com/56099627/74830132-cde6c500-5355-11ea-9ecf-cd6e4c29a617.png)  
  
![image](https://user-images.githubusercontent.com/56099627/74830178-ea82fd00-5355-11ea-84f1-143d0bc5dfb3.png)  

![image](https://user-images.githubusercontent.com/56099627/74891412-5010d100-53ca-11ea-8c54-2806b53d4021.png)  
  
- 이부분을 변경했음 그 결과  
D:\caffe\cmake\WindowsDownloadPrebuiltDependencies.cmake 에서  
이전(f060403fd1a7448d866d27c0e5b7dced39c0a607) -> 변경(d04c905437d24bf5fe629829ecbebb94713c6724)  

    set(DEPENDENCIES_URL_1900_35 "${DEPENDENCIES_URL_BASE}/v${DEPENDENCIES_VERSION}/${DEPENDENCIES_NAME_1900_35}${DEPENDENCIES_FILE_EXT}")
    set(DEPENDENCIES_SHA_1900_35 "d04c905437d24bf5fe629829ecbebb94713c6724")
  
![image](https://user-images.githubusercontent.com/56099627/74897614-fc5ab380-53da-11ea-9869-8cd837fadcb3.png)  
![image](https://user-images.githubusercontent.com/56099627/74897659-1a281880-53db-11ea-81f9-f6ed2f7fdd6a.png)  
![image](https://user-images.githubusercontent.com/56099627/74897720-43e13f80-53db-11ea-9706-cc2bb5b32904.png)  
![image](https://user-images.githubusercontent.com/56099627/74897751-607d7780-53db-11ea-9e2b-a6aaddd640b8.png)  





------------------------------------------------------
### caffe 셋업 잘 안된 케이스

git clone https://github.com/BVLC/caffe.git  
cd caffe  
cp Makefile.config.example Makefile.config (해당 폴더-파일 들어가서 수정하기!)  

    < 아나콘다 파이썬을 사용한다면 이 부분 찾아 **주석 처리** 하기 >
    Makefile.config 파일에서 두가지만 체크!
    CPU_ONLY := 1
    PYTHON_INCLUDE := /usr/local/include/python2.7 \
                                              /usr/local/include/python2.7/numpy

    < 아나콘다 파이썬을 사용한다면 이 부분 찾아 **주석 해제** 하기 >
    ANACONDA_HOME := $(HOME)/anaconda 
    PYTHON_INCLUDE := $(ANACONDA_HOME)/include \ 
      # $(ANACONDA_HOME)/include/python2.7 \ 
      $(ANACONDA_HOME)/lib/python2.7/dist-packages/numpy/core/include \

    # We need to be able to find libpythonX.X.so or .dylib. 
    # PYTHON_LIB := /usr/lib PYTHON_LIB := $(ANACONDA_HOME)/lib

# OpenBLAS 셋업
참고 2  
https://seonho.gitbooks.io/deep-learning-with-python/chap1/native/OpenBLAS.html  
![image](https://user-images.githubusercontent.com/56099627/74723655-4da16080-527e-11ea-8f7c-bd4bdfec5602.png)  

# boost 셋업
D:/openpose_caffe_train-master  
D:/openpose_caffe_train-master/build  
이렇게 빌드 시키려고 하니 아래 그림과 같이 오류가 떴다.  
보니, boost을 설치하랜다  
![image](https://user-images.githubusercontent.com/56099627/74799580-488ef080-5314-11ea-9603-284f66abfb21.png)
- 참고 1: https://wendys.tistory.com/115
- 참고 2: https://redcoder.tistory.com/143
- step 1) boost 다운로드
  - boost 다운로드 받는 공식 사이트 : https://www.boost.org/users/download/
- step 2) 다운로드 받은 것을 압축 해제 한다음 (경로 결과: D:\boost_1_72_0 ) **boostrap.bat 실행 하면 b2.exe, cjam.exe 파일 생성됨**
  - 나의 경우엔 b2.exe, cjam.exe 파일이 ./ 경로에 바로 생성되지 않아서 검색해보니 ./../engine/ 경로에 이 두개 파일이 생성되어서 이것을 ./ 복사해서 경로 밖으로 빼어 주었음(빼준 이유는 다음 step 실행하기 위해서) 
- step 3) 명령 프롬프트 **C:\Program Files (x86)\boost\boost_1_72_0>** 으로 들어간다. 그런후 아래 명령어를 실행하면 빌드 된다. 
  - 명령 프롬프트에서 명령어: **b2 --toolset=msvc-14.0 variant=debug,release address-model=64 threading=single,multi runtime-link=static,shared**
  - 32bit (x86) 빌드(vs2015) 쓰는 사람은 --toolset=msvc-14.0, address-model=32 이렇게 작성
  - 64bit (x86) 빌드(vs2015) 쓰는 사람은 --toolset=msvc-14.0, address-model=64 이렇게 작성 
- 참고! 참고 2 에서 알려준 방법인데 boost을 직접 빌드 하기 시르면 https://sourceforge.net/projects/boost/files/boost-binaries/ 으로 가서 빌드된 것을 다운로드 받으랜다.

두번째 에러
https://sourceforge.net/projects/boost/files/boost-binaries/ 에서 **boost_1_71_0-msvc-14.0-64.exe**을 다운로드 받은 후,  
C:/local/boost_1_17_0 경로로 설치 하였더니 아래 그림과 같은 에러 메세지 뜸  
![image](https://user-images.githubusercontent.com/56099627/74816686-f3b49f80-533e-11ea-9da1-e06bb741867d.png)  

- windows powershell 관리자 권한으로 들어가서 choco 을 설치함
  - 명령어: PS C:\Windows\system32> **Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))**
  - choco 버전 확인 : 명령어 **choco -v**, sudo 설치 명령어 : **choco install sudo**  
  
![image](https://user-images.githubusercontent.com/56099627/74817181-d6cc9c00-533f-11ea-899c-310e00c9ef4c.png)  
