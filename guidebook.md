# XEMA系列相机搭建指南

## V1.4.0

![image](https://user-images.githubusercontent.com/117330523/221456893-7206fbbc-9517-417c-a3ba-2378f17d7cf4.png)

## 一、准备工作

### 1.光机操作

1)光机调焦

可通过相机装配的电源线连接好光机的12V电源，用USB转I2C转接线连接PC与光机，上电后在PC端打开TI的DLP GUI软件，界面如下（新版本的GUI工具可切换光机类型，点击界面EVM Selection进入后可选择），点下右下角的Get，则右侧显示光机的型号和内部软件版本等信息。

![image](https://user-images.githubusercontent.com/117330523/221456913-6892ea74-9ff6-4a43-94c2-76ad0f1094ac.png)

按照下图的步骤设置光机，当棋盘格显示在墙面或白板上时，手动调焦使图案清晰，直至像素点清晰可见，光机与墙面的距离为相机最终使用的工作距离。

![image](https://user-images.githubusercontent.com/117330523/221456928-18dac19d-7821-4686-b888-87b0a026fe07.png)

2)图案生成

PC需要安装python，在下载的相机软件目录下找到tools文件夹，运行其中的create_patterns.py（适用3010光机），会在tools文件夹里创建 patterns文件夹，内中有生成的42幅条纹图案，其中垂直正弦条纹18幅、水平正弦条纹18幅、灰度图6幅。

![image](https://user-images.githubusercontent.com/117330523/221456943-8ee27bfa-c473-4fe6-922b-d4ecd53d3a18.png)

![image](https://user-images.githubusercontent.com/117330523/221456961-7a89ad68-5f02-4c2a-9d37-56c26c2057ab.png)

3)写入光机

将上一步骤中生成的42幅图片，每6个一组，分组添加到GUI工具软件中，注意Vertical对应竖条纹，Horizontal对应横条纹，操作如下图：

![image](https://user-images.githubusercontent.com/117330523/221456978-96330c88-b205-43bb-90eb-52e3978302ef.png)

![image](https://user-images.githubusercontent.com/117330523/221456993-536572ca-1912-4bfe-bd22-18c74f480202.png)

![image](https://user-images.githubusercontent.com/117330523/221457013-18b61c79-e4e4-4775-b337-5f42c1aeb0b2.png)

![image](https://user-images.githubusercontent.com/117330523/221457032-271294c0-a4c6-4d20-91d0-9b242ad41792.png)

后面依照这个方式将剩余的6组图片依次添加进来，注意3组之后就是横条纹，添加时注意选择是Horizontal Pattern，最后的6幅无条纹灰度图Horizontal/Vertical两种方式都可以。全部添加完后，点击下一步，配置每一组图案的曝光参数。

![image](https://user-images.githubusercontent.com/117330523/221457052-df4af814-92c2-4acf-a677-72e674204517.png)

![image](https://user-images.githubusercontent.com/117330523/221457062-18d559df-6af1-4a26-b12a-d1f336e80f51.png)

![image](https://user-images.githubusercontent.com/117330523/221457072-037a5784-6066-499d-b94f-46f937066d2e.png)

全部配置完后，点击Program and Load Pattern将图片和参数写入光机，完成后点击下一步可以测试。

![image](https://user-images.githubusercontent.com/117330523/221457096-9528a245-63ab-4d46-ba6d-4c7d47713897.png)

### 2.Nano系统安装（Jetson Nano Moudle）

Nvidia官方网站“Jetson Nano开发者套件入门”，对安装和启动有详细的介绍，需要留意的是相机通过直流电源插座给Jetson Nano供电，因此载板上的J48需要用跳线短接。

Jetson Nano的官方载板需将J50的Pin9和Pin10用跳线帽短接，短接位置见下图。

![image](https://user-images.githubusercontent.com/117330523/221457115-869ded16-e32c-467b-840b-f2fd8992eb6f.png)

![image](https://user-images.githubusercontent.com/117330523/221457129-1c7632a4-6499-4930-946f-dfb82c0b72fc.png)

将Jetson Nano Module安装在官方载板上，连接5V DC电源、HDMI显示器、USB鼠标和键盘、网线、Micro-B USB线至Linux主机，并给5V电源上电。

![image](https://user-images.githubusercontent.com/117330523/221457150-5a99e58e-c1de-4c1c-9f91-a01be5910aa7.png)

通过安装了SDKManager的Linux主机，安装系统至Nano Module，首先打开SDKManager，登录需要数秒钟（Linux主机的版本必须为Ubuntu18.04，高版本下SDKManager的安装过程是无法进行的）。

![image](https://user-images.githubusercontent.com/117330523/221457169-34f57b30-fef0-4e28-a1a3-06a3a187fa08.png)

登录成功后，弹出提示，选择硬件，按图选择Jetson Nano，点击OK。

![image](https://user-images.githubusercontent.com/117330523/221457181-3ac9f38a-d8b9-40ff-a4ac-02d746bf1daf.png)

按图选择，将“Host Machine”的勾去掉，点击“CONTINUE”进入下一步。

![image](https://user-images.githubusercontent.com/117330523/221457203-484b4298-6935-4ca1-8f26-1685b247006b.png)

勾选下方的接受协议，点击下一步。

![image](https://user-images.githubusercontent.com/117330523/221457219-7cf740c8-4472-4359-abc6-2ff4e8a08481.png)

首次安装需要生成下载路径，点击“Create”。

![image](https://user-images.githubusercontent.com/117330523/221457242-7c5985a9-5272-4038-a1ff-031f40f52b3c.png)

要求填写用户密码，填写：dexforce。

![image](https://user-images.githubusercontent.com/117330523/221457249-c0e08840-19cf-4b8d-92e7-7dd511d2140b.png)

填写完后，开始安装，时间约需要1个小时，安装过程中需要有一些操作，按照提示进行操作。

![image](https://user-images.githubusercontent.com/117330523/221457272-b5d71b6e-3086-4928-b900-5c3a218c19d2.png)

Jetson Nano的系统下载完后，正式烧写之前会有提示，强制恢复模式选择手动方式，将第一步中J50的跳线帽去掉，填写用户名、密码，点击“Flash”开始烧写。

![image](https://user-images.githubusercontent.com/117330523/221457295-dfe9f489-0340-47f6-a3aa-d4ff9252d2f2.png)

![image](https://user-images.githubusercontent.com/117330523/221457332-b5ca31cd-ae1e-461a-b1b0-02db87688cbe.png)

Jetson Nano的Ubuntu系统安装完后，板子会启动，HDMI显示器会点亮，主机的SDKManager界面会有提示，可以先输入用户名和密码，但不要“Install”，需要对Nano系统进行必要的设置。

![image](https://user-images.githubusercontent.com/117330523/221457354-60228e08-0fad-4670-9890-f2d83fa9ca35.png)

Nano系统启动后会弹出系统配置对话框，如图勾选并继续，语言和键盘均选择默认英语，地区点击地图中的位置，显示“Shanghai”并点击“Continue”，接下来用户名填写：
dexforce，密码和确认密码均为：dexforce；然后继续点击“Continue”至配置完成，进入系统界面。

![image](https://user-images.githubusercontent.com/117330523/221457373-fd31a172-59ad-4b64-9b73-9f00dd75c846.png)

![image](https://user-images.githubusercontent.com/117330523/221457411-1192e967-a755-42b0-b8f2-0381a286f41f.png)

![image](https://user-images.githubusercontent.com/117330523/221457385-6ea732c6-15d1-47a5-ae78-62abb0e346b7.png)

![image](https://user-images.githubusercontent.com/117330523/221457455-3cf9175d-deee-451e-9ba4-001e7fd8da3c.png)

![image](https://user-images.githubusercontent.com/117330523/221457484-4a89b81f-43fb-49b3-8a5c-1e5907ce771a.png)

主机端点击“install”继续安装，SDK组件安装完成后，整个安装过程完成，SDKManager 界面会有提示安装成功，点击“FINISH”退出。

## 二、整机组装

### 1.组件安装

斜插入载板260PIN座子中，听两边卡簧复位证明装到位，并用十字螺丝刀将2个M2.5*5的螺丝固定到PCB板上。

![image](https://user-images.githubusercontent.com/117330523/221457567-9e1f82c1-aac0-416b-9043-dc295e609138.png)

依次将镜头旋入相机卡口，将滤光片旋入镜头卡口。

![image](https://user-images.githubusercontent.com/117330523/221457605-8588c375-3cc7-413e-9e17-da4f7250d771.png)

![image](https://user-images.githubusercontent.com/117330523/221457620-79cebdcc-e69d-40ad-a75d-5bc3da3411df.png)

将相机组件如图示平放桌面，将相机背板安到相机上，用内六角扳手将3个KM3*6螺丝拧到箭头所指位置。

![image](https://user-images.githubusercontent.com/117330523/221457660-02d91917-a72c-4b58-a218-dc2336f6d15f.png)

将相机组件如图示平放桌面，将触发线插到触发线插线端口，同时把螺母拧紧，把USB线底部的一螺丝取出，将只有一个固定螺丝的USB线插到USB插线端口，同时拧紧剩下的一个螺丝。

![image](https://user-images.githubusercontent.com/117330523/221457711-ab45deb1-bf3a-4e8d-9c68-b2d4237f83a5.png)

### 2.整机组装

将底壳底朝上平放桌面如图所示，把脚垫分别粘到底壳如图箭头所指位置

![image](https://user-images.githubusercontent.com/117330523/221457757-b953f03c-e71b-4c71-834d-c83dd2849e83.png)

将防水圈套到航插螺纹上，底壳底朝下平放桌面如图所示，将套好防水圈的航插带线一端插入底壳，把M16螺母穿过线到航插螺纹，用手拧紧，手拧不动后再用扳手加固。

![image](https://user-images.githubusercontent.com/117330523/221457805-d4857a90-fc4c-44d3-99be-ac450bc24578.png)

底壳如图所示平放台面，将铜螺柱分别拧到如图所示的2处位置，用手拧不动后再用M3套筒加固。

![image](https://user-images.githubusercontent.com/117330523/221457868-8db11429-6c2b-47fb-842f-09b586975e5c.png)

将调焦环套到光机镜头上，贴好导热硅胶，装好调焦套筒的光机组件如图所示装到底壳上，并用3个螺丝将光机组件固定紧。

![image](https://user-images.githubusercontent.com/117330523/221457968-ab4a0a0a-5dcf-40d2-b7aa-6ba51d67161f.png)

把调焦手柄装到图示位置，将2个M3*6内六角螺丝固定到如图示位置，M3*4机米螺丝用内六角扳手固定到图示位置。

![image](https://user-images.githubusercontent.com/117330523/221458043-80186002-b3c1-4b3c-a35e-647aea8d2925.png)

将相机组件装到图示位置，用3个M3*6内六角螺丝固定。

![image](https://user-images.githubusercontent.com/117330523/221458084-513dd216-634d-4cd3-b721-43cdd7654d3f.png)

剪出合适大小的导热硅胶，撕掉一面保护膜，贴到图示位置，然后再撕掉另外一面保护膜，光机排线插到图示位置，同时在排线连接处涂上黄胶。

![image](https://user-images.githubusercontent.com/117330523/221458128-d1703ea2-ecf6-4f2d-a163-05dc546e6141.png)

将光机排线插到驱动板接口，然后把驱动板安装至对应位置，用4个M2*6机牙螺丝将光机驱动板固定，将光机FPC线压到驱动板接线端口，贴上黑色胶片，压上不锈钢片，用2个M1.7半牙螺丝把不锈钢片固定到光机驱动板上。

![image](https://user-images.githubusercontent.com/117330523/221458173-d3da0881-c80b-41ec-9531-763984035b21.png)

将核心板组件安装到底壳上，用内六角扳手将4个M3*6内六角螺丝打到箭头所指位置。

![image](https://user-images.githubusercontent.com/117330523/221458233-785127fc-1d16-4b86-8756-f698972bc485.png)

1、如图所示，将电源线、I2C线、触发线、USB线、温感线连接至对应接口。

![image](https://user-images.githubusercontent.com/117330523/221458289-737413f9-ef2d-4ff7-855e-5a172d7b4e2d.png)

线接好后，为防止松脱，加黄胶固定。

![image](https://user-images.githubusercontent.com/117330523/221458347-12471948-4f94-4444-aa5f-24a304047a60.png)

将清理干净的镜片，有丝印的那面对着底壳打了胶的沉台按压进去，用无尘布将溢出的胶擦拭干净。

![image](https://user-images.githubusercontent.com/117330523/221458426-2f7d0bb2-d8e9-478d-8601-e58968df3785.png)

![image](https://user-images.githubusercontent.com/117330523/221458452-d3f3cd97-1a3f-4f84-9c17-f920cd505604.png)

装好的底壳组件，用风枪把内部的杂物，灰尘吹干净之后平放在桌面，将上壳安装到底壳组件上，用内六角扳手将5个KM3*8螺丝打紧。

![image](https://user-images.githubusercontent.com/117330523/221458492-43fff8cc-7d58-4d15-9c3e-21cb701c5572.png)

## 三、软件安装

请将相机连接到有路由器的网络中，保证相机接入互连网，通过ssh服务进入Jetson Nano。执行以下命令安装相机软件：

git clone https://gitee.com/open3dv/install.git

![image](https://user-images.githubusercontent.com/117330523/221458580-e165065d-1b05-48f2-a0ee-4b180e316e11.png)

cd install/

sudo chmod +x install.sh

sudo ./install.sh

![image](https://user-images.githubusercontent.com/117330523/221458635-d429248c-d385-493e-9366-25292c0de83e.png)

回车

y 回车

en 回车

y 回车

y 回车

![image](https://user-images.githubusercontent.com/117330523/221458782-5ec0793e-a139-4c63-a0c7-efc4e3f524d0.png)

y 回车

y 回车

![image](https://user-images.githubusercontent.com/117330523/221458822-82f744bc-674a-479b-82a2-bba22f1b1978.png)

开始下载、编译程序：

![image](https://user-images.githubusercontent.com/117330523/221458863-a63dff8a-4cdf-4a13-aae6-3856c5f2c36b.png)

![image](https://user-images.githubusercontent.com/117330523/221458910-6b808aaa-d8f1-4814-92bf-3900f6258cde.png)

至处，安装成功！

指令说明：

下面是下载安装相机驱动，有大恒相机驱动和Basler相机驱动。

cd

git clone https://gitee.com/open3dv/galaxy-linux-armhf.git

cd galaxy-linux-armhf

tar xvf Galaxy_Linux-armhf_Gige-U3_32bits-64bits_1.3.2111.9261.tar.gz

cd Galaxy_Linux-armhf_Gige-U3_32bits-64bits_1.3.2111.9261

sudo ./Galaxy_camera.run

cd

rm -rf galaxy-linux-armhf

cd

git clone https://gitee.com/open3dv/basler_linux_arm64.git

cd basler_linux_arm64/

sudo tar -C /opt/pylon -xzf ./pylon_*.tar.gz

sudo chmod 755 /opt/pylon

sudo /opt/pylon/share/pylon/setup-usb.sh
cd

rm -rf basler_linux_arm64/

下面是设置环境变量命令：

export CUDA_HOME=/usr/local/cuda

export LD_LIBRARY_PATH=${CUDA_HOME}/lib64:${LD_LIBRARY_PATH}

export PATH=${CUDA_HOME}/bin:${PATH}

下面是编译固件：首先下载相机固件和第三方库，接着要生成版本文件，然后进行编译，流程如下所示。

cd

git clone https://gitee.com/open3dv/xema.git --depth=1 -b dev

git clone https://gitee.com/open3dv/thirdparty.git --depth=1 

mkdir xema/3rdparty

cp -r thirdparty/linux-opencv-4.4.0 xema/3rdparty

cp -r thirdparty/JetsonGPIO xema/3rdparty

rm -rf thirdparty

cd xema/version

chmod +x build.sh

./build.sh

cd ../firmware

mkdir build

cd build

cmake ..

make -j4

cp /home/dexforce/xema/3rdparty/linux-opencv-4.4.0/lib/* .

cd 

git clone https://gitee.com/open3dv/ConfiguringIP.git

cd ConfiguringIP/firmware

mkdir build

cd build

cmake ..

make -j4

开机启动：

打开文件：sudo vim /etc/rc.local

第一行必须为：#!/bin/bash，没有则添加

在文件末尾添加：

cd /home/dexforce/xema/firmware/build 

./camera_server &

cd /home/dexforce/ConfiguringIP/firmware/build

./configuring_ip &

将文件属性更改为可执行：

sudo chmod +x xema/firmware/build/camera_server

sudo chmod +x ConfiguringIP/firmware/build/configuring_ip

sudo chmod +x /etc/rc.local

## 四、客户端软件编译

Windows客户端的开发基于Microsoft Visual Studio Community 2019，可以从微软的官方网站登录下载：

https://my.visualstudio.com/Downloads?q=visual%20studio%202019&wt.mc_id=o~msft~vscom~older-downloads。

客户端界面使用Qt工具设计，版本为Qt5.9.3。

源码下载管理工具为git，没有特别的版本要求。

Windows平台下的shell运行环境，需安装Cygwin，没有特别的版本要求。

### 1.Xema

下载源代码：

git clone https://gitee.com/open3dv/xema.git -b dev

下载完成后，进入xema目录，下载第三方库：

git clone https://gitee.com/open3dv/thirdparty.git 3rdparty

![image](https://user-images.githubusercontent.com/117330523/221459701-7b081c7c-3a26-41de-bfb7-e8f83227355d.png)

双击OpenCam3D.sln打开客户端源码的VC解决方案，并进行必要的配置：

![image](https://user-images.githubusercontent.com/117330523/221459752-40ed449f-c7b2-4944-ae20-53b6837534e4.png)

编译开关设置为Release：

![image](https://user-images.githubusercontent.com/117330523/221459768-3e5a4f92-66ef-4b0f-a197-bba86e5e5e81.png)

Qt插件安装：

在VS2019的菜单栏选择“扩展” —— “管理扩展”，在弹出的界面中点击左侧的“联机”，然后在右侧搜索框输入“Qt”并回车，界面中间出现“Qt Visual Studio Tools”，点击选中该条目，此时条目右上角出现“下载”按钮，点击下载开始下载和安装，安装完成后如图所示。

![image](https://user-images.githubusercontent.com/117330523/221459787-daf10c4d-f164-485c-8014-256e81a44362.png)

Qt版本设置：

在菜单栏点击“扩展” —— “Qt VS Tools” —— “Qt Versions”，在弹出的界面中配置Qt的编译器版本，先点击“Path”在弹出的对话框中选择Qt编译器的路径，再设置前面的“Version”，设定好之后点击“确定”。

![image](https://user-images.githubusercontent.com/117330523/221459802-23d2eb47-4596-477b-8684-4d23c76ce45d.png)

![image](https://user-images.githubusercontent.com/117330523/221459819-4c4cdb7b-67e0-4727-8360-0727d2cae0dc.png)

编译执行：

在VS2019解决方案界面右侧（也可能是在左侧，取决于设置），“解决方案‘OpenCam3D’”上点击鼠标右键，并在“生成解决方案”上点击鼠标左键开始编译过程。

![image](https://user-images.githubusercontent.com/117330523/221459853-43a52231-5591-487e-9840-21e2bfed89e5.png)

![image](https://user-images.githubusercontent.com/117330523/221459876-32e4234d-1a52-4f98-ad49-122bc51e6c36.png)

生成的文件：

在xema解决方案文件夹下，x64\Release目录下，具体软件的使用可以参考《XEMA系列相机使用手册》

![image](https://user-images.githubusercontent.com/117330523/221459939-898b4826-8984-4710-b05b-746f9e3574f0.png)

![image](https://user-images.githubusercontent.com/117330523/221459957-36e5c20a-3c7d-4bb5-b6c6-12c637dd8508.png)

### 2.ConfiguringIP

下载源代码：

git clone https://gitee.com/open3dv/ConfiguringIP.git

双击ConfiguringIP.sln打开客户端源码的VC解决方案，并进行必要的配置，整个配置过程与xema解决方案的配置过程完全一致。

生成的文件：

同样和xema一致，在解决方案的x64\Release目录下，因执行同样要依赖Qt的动态库，所以建议可将configuring_ip.exe和configuring_network_gui.exe拷贝至xema编译之后的Release文件夹内，再运行操作。

## 五、相机标定

### 1.标定操作

1)根据相机工作距离，准备好相应规格的标定板；

2)标定要拍摄N组图片，使用上位机软件open_cam3d.exe拍照获取，在命令行窗口中执行该软件，可以看到命令的使用方法：

.\open_cam3d.exe

3)将标定板放置在距离相机适当的位置（取决于工作距离），执行拍照命令，获取一组图片（相机的IP地址需要改为实际分配的地址）:

./open_cam3d.exe --get-raw-02 --ip 192.168.x.x --path .\capture\00

4)在目标工作距离的约正负15%的范围内，变换标定板位姿，运行拍照命令，获取第二组图片：

./open_cam3d.exe --get-raw-02 --ip 192.168.x.x --path .\capture\01

接着重复以上操作，得到至少00~24组拍摄的图片。

5)运行标定程序自动进行相机标定（这里需要注意标定板的规格设置），标定完成后，会在当前目录下生成标定参数文件param.txt：

.\calibration.exe --calibrate --use patterns --path ./capture/ --version 3010 --board 20 --calib ./param.txt

6)运行命令将标定结果写进相机：

.\open_cam3d.exe --set-calib-looktable --ip 192.168.x.x --path ./param.txt

### 2.点云获取

运行命令获取一帧点云数据在指定目录下（下面的示例为frame_03），一帧数据有三个文件组成，其中.bmp为亮度图、.tiff为深度图、.xyz为点云数据。

.\open_cam3d.exe --get-frame-04 --ip 192.168.x.x --path ./frame_04

修订记录

V0.5			2022.11.3			整理已有文档，并补充完善。

V0.6			2022.11.5			完善软件安装部分。

V0.7          2022.11.22			补充客户端软件编译部分。