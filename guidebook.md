# XEMA系列相机搭建指南

## V1.5.1

![image](https://user-images.githubusercontent.com/117330523/221456893-7206fbbc-9517-417c-a3ba-2378f17d7cf4.png)

## 一、准备工作

### 1、光机操作（DIY出货已提前烧录好，可直接跳过此步骤）

1)烧图准备

可通过相机装配的电源线连接好光机的12V电源，用USB转I2C转接线连接PC与光机，

![image](https://github.com/Open3DV/Xema/assets/117330523/79f62147-8bae-4bdc-b478-452ea009d96a)


上电后在PC端打开TI的DLP GUI软件，界面如下（新版本的GUI工具可切换光机类型，点击界面EVM Selection进入后可选择），点下右下角的Get，则右侧显示光机的型号和内部软件版本等信息。

![image](https://github.com/Open3DV/Xema/assets/117330523/e36ab348-cbdd-4acc-ad24-9d2d3f8d2879)


2)图案生成（需生成2次）

① PC需要安装python，在下载的相机软件目录下找到tools文件夹，运行create_patterns.py（适用3010光机），会在tools文件夹里创建 patterns文件夹，内中有生成的42幅条纹图案，其中垂直正弦条纹18幅、水平正弦条纹18幅、灰度图6幅。

![image](https://github.com/Open3DV/Xema/assets/117330523/a87b26c4-4b36-456a-9ce6-e7b229ba0d68)

![image](https://github.com/Open3DV/Xema/assets/117330523/8f2007cf-7ab3-4f16-b780-22ba21d72b4c)

② 同样在tools文件夹中，打开终端运行create_minsw_code.py（适用3010光机），会在tools文件夹里创建 patterns_minsw_code文件夹，其中有生成的10幅图案，其中竖条纹图案8幅（00-07）、纯黑图案1幅，纯白图案一幅。

![image](https://github.com/Open3DV/Xema/assets/117330523/dc59e67c-2fb7-4e4e-892e-cfb0fd7881ea)

![image](https://github.com/Open3DV/Xema/assets/117330523/604484b1-eb55-4067-95b1-4dd407341a9a)


3)写入光机（patterns+patterns_minsw_code条纹均添加写入）

① 先将patterns文件夹中的42幅图片，每6个一组，分组添加到DLP软件中，注意Vertical对应竖条纹，Horizontal对应横条纹，横竖条纹都选择8-bit，具体操作如下图：

![image](https://github.com/Open3DV/Xema/assets/117330523/47a1c6fe-d7f8-4c54-8ba9-3d920c1bf704)

![image](https://github.com/Open3DV/Xema/assets/117330523/f3db4a4f-b960-461b-b75e-94652d848012)

![image](https://github.com/Open3DV/Xema/assets/117330523/c161e9d5-6152-40df-8a65-724c2e0afe0c)

![image](https://github.com/Open3DV/Xema/assets/117330523/e93b7ba6-31ce-4c1b-bf8a-c747db31fad8)

后面依照这个方式将剩余的6组图片依次添加进来，注意3组之后就是横条纹，添加时注意选择是Horizontal Pattern，最后的6幅无条纹灰度图Horizontal/Vertical两种方式都可以。

② 再将patterns_minsw_code文件夹中的10幅图片，8个竖条纹为一组，2个黑白条纹为一组，将两组分别添加到DKP软件中，两组都选择Vertical 1-bit，具体操作如下图：

![image](https://github.com/Open3DV/Xema/assets/117330523/68525fad-baf0-4381-b928-c16acec3f776)

![image](https://github.com/Open3DV/Xema/assets/117330523/988abc52-b2af-48f2-9792-d213d0fac7b0)

![image](https://github.com/Open3DV/Xema/assets/117330523/140284c3-f3a3-4b0b-9325-4cd8e683e926)

全部添加完后，点击下一步，对于前7组配置每一组图案的曝光参数如下。

![image](https://github.com/Open3DV/Xema/assets/117330523/7d665857-64d7-4228-ba46-925c2ceeeee2)

![image](https://github.com/Open3DV/Xema/assets/117330523/708b2ddb-26a9-4f34-a8a0-de0407de259b)

对于第8组和第9组配置每一组图案的曝光参数如下。

![image](https://github.com/Open3DV/Xema/assets/117330523/811ad738-0ae9-43c7-bec1-8e1722142105)


全部配置完后，点击Program and Load Pattern将图片和参数写入光机，完成后点击下一步可以测试。

![image](https://github.com/Open3DV/Xema/assets/117330523/99b32b20-650e-4eaa-a1fd-c4d2ad600657)

点击按钮Run Once，若光机投出正常条纹，说明烧图成功。

![image](https://github.com/Open3DV/Xema/assets/117330523/0ec5fde3-5927-40c3-b46f-7eca5d0af564)

### 2、Jetson Nano系统安装（DIY出货已提前烧录好，可直接跳过此步骤）

1、配置过程：

（Nvidia官方网站“Jetson Nano开发者套件入门”，对安装和启动有详细的介绍）

1）电脑主机的环境为 Ubuntu18.04，Jetson Nano 核心板安装至官方载板，用跳线帽设置载板为 RECOVERY 模式（载板J48用跳线短接），短接位置见下图红框标记位置：

![image](https://github.com/Open3DV/Xema/assets/117330523/22e4b644-5d5b-43cd-89a4-bd6f3184ae3a)

![image](https://github.com/Open3DV/Xema/assets/117330523/833caddd-333a-486d-8d6c-d1a56118d5e6)


2）将Jetson Nano Module安装在官方载板上，连接5V DC电源、HDMI显示器、USB鼠标和键盘、网线、Micro-B USB线至Linux主机，并给5V电源上电，如下图：

![image](https://github.com/Open3DV/Xema/assets/117330523/6ca5b8d5-e5e8-4446-966f-84be052e0d56)


3）通过安装了SDKManager的Linux主机，安装系统至Nano Module：首先打开SDKManager，登录（Linux必须为Ubuntu18.04，高版本下SDKManager的安装过程是无法进行的）；

![image](https://github.com/Open3DV/Xema/assets/117330523/0af43981-22a4-4ec7-9166-f52fe5ee5b4c)

4）登录成功后，弹出提示，选择硬件，按图选择Jetson Nano，点击OK；

![image](https://github.com/Open3DV/Xema/assets/117330523/15d9bbde-3eeb-41f3-8a74-c41dc0c9bd25)

5）依照下图选择，将“Host Machine”的勾去掉，选择Linux JetPack 4.6[rev.3]，然后点击“CONTINUE”进入下一步；

![image](https://github.com/Open3DV/Xema/assets/117330523/589945b4-faa9-43ff-9770-cac5cc484568)


6）勾选下方的接受协议（安装内容默认），点击下一步；

![image](https://github.com/Open3DV/Xema/assets/117330523/e7cdebab-fff9-4ff2-a34f-305da5a5dea3)

注意：首次安装需要生成下载路径，点击“Create”。

![image](https://github.com/Open3DV/Xema/assets/117330523/9ef49385-fc1b-4d83-8b40-75d6763cfa93)

7）弹框提示填写用户密码，密码：dexforce，开始安装；

![image](https://github.com/Open3DV/Xema/assets/117330523/8be98596-cbf1-4bf9-ba1b-8f30264a9558)

2、接下来的安装过程中有一些操作需要手动设置，请严格按照以下步骤进行操作：

1）下载安装一段时间后：Jetson Nano的系统下载完需要手动设置：①强制恢复模式选择手动方式；②填写用户名(dexforce)、密码(dexforce)，然后将第一步中J50的跳线帽去掉，点击“Flash”开始烧写；

![image](https://github.com/Open3DV/Xema/assets/117330523/4b08df4c-3c1c-4bd7-87ba-5c87cccbce46)

2）Jetson Nano的Ubuntu系统安装完后，板子也会启动，HDMI显示器会点亮，这时候需要对Nano系统进行一些必要的设置，具体设置如下：

Nano系统启动后会弹出系统配置对话框，如图勾选并继续，语言和键盘均选择默认英语，地区点击地图中的位置，显示“Shanghai”并点击“Continue”，接下来用户名填写：dexforce，密码和确认密码均为：dexforce；选择：Log in automatically，继续点击“Continue”至配置完成，进入系统界面。

![image](https://github.com/Open3DV/Xema/assets/117330523/af951e37-35fd-418a-bce5-97bd2800561a)

![image](https://github.com/Open3DV/Xema/assets/117330523/58c265c0-6493-4735-8f45-6d509a482388)

![image](https://github.com/Open3DV/Xema/assets/117330523/f58530f2-e40e-40f3-a8ba-c59e51146409)

![image](https://github.com/Open3DV/Xema/assets/117330523/d8be11f5-08eb-4538-ba2b-6d7cf8bf4012)

![image](https://github.com/Open3DV/Xema/assets/117330523/0d27e682-ed83-4c38-82bc-39b77ccd85d0)

3）Nano系统界面设置完成后，待完全Nano重启成功，回到主机的SDKManager界面：输入用户名dexforce和密码dexforce，点击“install”继续安装

![image](https://github.com/Open3DV/Xema/assets/117330523/258ef127-907a-4bf6-a980-b5a0eae177af)

所有设置均完成，整个安装过程大约需1小时左右，待完成后点击“FINISH”退出即完成安装。

## 二、整机硬件组装

### 1.组件安装

斜插入载板260PIN座子中，听两边卡簧复位证明装到位，并用十字螺丝刀将2个M2.5*5的螺丝固定到PCB板上。

![image](https://github.com/Open3DV/Xema/assets/117330523/1e5f0146-9266-47fd-810c-9c3f27c55c51)

依次将镜头旋入相机卡口，将滤光片旋入镜头卡口。

![image](https://github.com/Open3DV/Xema/assets/117330523/d8d98377-2bb4-416e-8927-7fa40311b52d)

![image](https://github.com/Open3DV/Xema/assets/117330523/745b3e3d-c7a3-499e-8c9d-bf020cc4a724)


将相机组件如下图所示平放桌面，将相机背板安到相机上，用内六角扳手将3个KM3*6螺丝拧到箭头所指位置。

![image](https://github.com/Open3DV/Xema/assets/117330523/d2e00ede-0cd4-4ec3-8554-f91492c305bd)


将相机组件如下图所示平放桌面，先安装将USB传输线，再将触发线插到触发线插线端口。

![image](https://github.com/Open3DV/Xema/assets/117330523/ea7a68d1-5c35-4292-834b-5f62b929b12a)


### 2.整机组装

将底壳底朝上平放桌面如下图所示，把脚垫分别粘到底壳如图箭头所指位置

![image](https://github.com/Open3DV/Xema/assets/117330523/8db50163-472d-4ce5-a6f6-4886ef1200df)

将防水圈套到航插螺纹上，底壳底朝下平放桌面如下图所示，将套好防水圈的航插带线一端插入底壳，把M16螺母穿过线到航插螺纹，用手拧紧，手拧不动后再用扳手加固。

![image](https://github.com/Open3DV/Xema/assets/117330523/16b25433-9684-40d0-9c08-e29329fcd03e)

底壳如图下所示平放台面，将铜螺柱分别拧到如图所示的2处位置，用手拧不动后再用M3套筒加固。

![image](https://github.com/Open3DV/Xema/assets/117330523/3e0c6b1d-4cc0-4c6b-9194-bb2147ef7724)

将调焦环套到光机镜头上，贴好导热硅胶，装好调焦套筒的光机组件如下图所示装到底壳上，并用3个螺丝将光机组件固定紧。

![image](https://github.com/Open3DV/Xema/assets/117330523/38ce6be7-8922-4c41-987b-1d223ae8668e)

把调焦手柄装到如下图所示位置，将2个M3*6内六角螺丝固定到如图示位置，M3*4机米螺丝用内六角扳手固定到图示位置。

![image](https://github.com/Open3DV/Xema/assets/117330523/311f3d74-a557-4ed4-86eb-f1e7a63e27c3)

将相机组件装到下图所示位置，用3个M3*6内六角螺丝固定（安装相机前建议可先调好光圈值）。

![image](https://github.com/Open3DV/Xema/assets/117330523/22bcbb43-3d54-431f-be6f-220313f7f521)

剪出合适大小的导热硅胶，撕掉一面保护膜，贴到图示位置，然后再撕掉另外一面保护膜，光机排线插到图示位置，同时在排线连接处涂上黄胶。

![image](https://github.com/Open3DV/Xema/assets/117330523/ec1b9e5c-d0ca-4bbd-b774-b68ee1064d04)

将光机排线插到驱动板接口，然后把驱动板安装下图所示中对应位置，用4个M2*6机牙螺丝将光机驱动板固定，将光机FPC线压到驱动板接线端口，贴上黑色胶片，压上不锈钢片，用2个M1.7半牙螺丝把不锈钢片固定到光机驱动板上。

![image](https://github.com/Open3DV/Xema/assets/117330523/899bae01-1512-4cb2-9824-ef6cbc9a1b38)

将核心板组件安装到底壳上，用内六角扳手将4个M3*6内六角螺丝打到下图中箭头所指位置。

![image](https://github.com/Open3DV/Xema/assets/117330523/5dc1d538-a0ad-4279-b261-9fbf2af3b325)

1、如下图所示，将24V电源线、I2C线、触发线、USB线、温感线连接至对应接口。

![image](https://github.com/Open3DV/Xema/assets/117330523/45c57342-79e1-4b68-8d1c-77fb53e6be7c)

线接好后，为防止接线口松脱，加工业粘胶剂固定。

![image](https://github.com/Open3DV/Xema/assets/117330523/48eb1887-2de2-416b-8ede-d8b640a58b7a)

将清理干净的镜片，有丝印的那面对着底壳打了胶的沉台按压进去（如下图所示），用无尘布将溢出的胶擦拭干净。

![image](https://github.com/Open3DV/Xema/assets/117330523/ecf135d5-24fd-4187-9ad0-1edf6a4c1236)

![image](https://github.com/Open3DV/Xema/assets/117330523/e89751e3-c68a-4144-a2cc-89b609f7cdcc)

装好的底壳组件，可使用吹尘球把内部的杂物，灰尘吹干净之后平放在桌面，将上壳安装到底壳组件上，用内六角扳手将5个KM3*8螺丝打紧（如下图所示）。

![image](https://github.com/Open3DV/Xema/assets/117330523/d37bc0e9-8127-4bdf-9549-641c19efbbd4)

## 三、相机下位机软件安装

请将相机连接到有路由器的网络中，保证相机接入互连网，电脑同样接入互联网，登录本地路由，例如：192.168.3.1，通过核心板上的MAC地址的后4位搜索到相机的IP， 通过ssh服务进入Jetson Nano，如：ssh [dexforce@192.168.3.41](mailto:dexforce@192.168.3.41,)

执行以下命令安装相机软件：

git clone https://gitee.com/open3dv/install.git

![image](https://github.com/Open3DV/Xema/assets/117330523/e8b21d25-6a1e-455f-9396-017e88c9264a)

cd install/    （### 进入install文件夹）

chmod +x install.sh     （### 给install.sh附加执行权限）

./install.sh    （### 执行install.sh脚本安装软件）

![image](https://github.com/Open3DV/Xema/assets/117330523/ffec2267-32e6-4942-ac9e-400e78394cbd)

根据提示依次：enter键回车 → y回车 → en回车 → y回车 → y回车

![image](https://github.com/Open3DV/Xema/assets/117330523/83341251-efcf-4c1d-a047-cb7d8a94ce20)

![image](https://github.com/Open3DV/Xema/assets/117330523/b330dbf7-9788-4d65-8db8-82500abb2f89)

![image](https://github.com/Open3DV/Xema/assets/117330523/119b960c-b29d-4c60-b13f-82801cf338f9)

![image](https://github.com/Open3DV/Xema/assets/117330523/78e5f6d8-59f5-4c51-bc75-312313e6f2a5)

以下是相机软件安装install.sh的指令说明，不需操作，用户可直接跳至步骤四。

① 设置环境变量命令

![image](https://github.com/Open3DV/Xema/assets/117330523/cd299afa-941b-492e-be6d-8b662e8fb38e)

② 下载安装相机驱动，有大恒相机驱动和Basler相机驱动。

![image](https://github.com/Open3DV/Xema/assets/117330523/24facc47-bcb1-4dd8-84ac-65db417cf318)

③ 编译固件（xema+ConfiguringIP)：首先下载相机固件和第三方库，接着要生成版本文件，然后进行编译，流程如下所示：

![image](https://github.com/Open3DV/Xema/assets/117330523/dd80412d-6a63-45ec-987b-7e0f31bcb594)

④ 设置开机启动项：

![image](https://github.com/Open3DV/Xema/assets/117330523/4d2535d8-42c5-4b0a-8e2e-82f2429b9a3e)

至处，软件安装已完成，进入配置检查

1，进行相机网络配置：https://gitee.com/open3dv/ConfiguringIP/wiki

根据如下图中分别配置interfaces/networking_service/dhclient.conf/NetworkManager.conf

![image](https://github.com/Open3DV/Xema/assets/117330523/5ec9dcca-d84f-4f14-a895-ac5183bd7180)


2，配置cron服务，每分钟查询一次

crontab -e

最末尾添加：*/1 * * * * /opt/xema/restart_camera.sh

![image](https://github.com/Open3DV/Xema/assets/117330523/a76004e8-cc3c-42b2-9534-493f8e48cff8)

注意检查restart_camera.sh脚本的位置，比如：如果restart_camera.sh脚本在/opt/xema下，则应该将/home/dexforce/xema改为/opt/xema切记！切记！

## 四、PC客户端软件编译

（PC客户端也可从网址：https://gitee.com/open3dv/xema/releases直接下载发行版安装包即可使用）

Windows客户端的开发基于Microsoft Visual Studio Community 2019，可以从微软的官方网站登录下载：

https://my.visualstudio.com/Downloads?q=visual%20studio%202019&wt.mc_id=o~msft~vscom~older-downloads。

客户端界面使用Qt工具设计，版本为Qt5.9.3。

源码下载管理工具为git，没有特别的版本要求。

Windows平台下的shell运行环境，需安装Cygwin，没有特别的版本要求。

### 1.Xema 编译（上位机GUI）

PC端任意选择一个路径打开终端执行以下语句下载源代码：

git clone [https://gitee.com/open3dv/xema](https://gitee.com/open3dv/xema.git) -b dev

下载完成后，cd xema/进入目录，打开终端执行以下语句下载第三方库：

git clone [https://gitee.com/open3dv/thirdparty](https://gitee.com/open3dv/thirdparty.git) 3rdparty

![image](https://github.com/Open3DV/Xema/assets/117330523/7402e189-39d9-4506-9b19-6cc16fb531ec)

双击OpenCam3D.sln打开客户端源码的VC解决方案，并进行必要的配置：

![image](https://github.com/Open3DV/Xema/assets/117330523/31be5c8b-d510-4cd6-9179-f7c86711ca15)

编译开关设置为Release：

![image](https://github.com/Open3DV/Xema/assets/117330523/aed295b7-3993-4904-b0f4-520d22bf0f93)

Qt插件安装：

在VS2019的菜单栏选择“扩展” —— “管理扩展”，在弹出的界面中点击左侧的“联机”，然后在右侧搜索框输入“Qt”并回车，界面中间出现“Qt Visual Studio Tools”，点击选中该条目，此时条目右上角出现“下载”按钮，点击下载开始下载和安装，安装完成后如图所示。

![image](https://github.com/Open3DV/Xema/assets/117330523/9ea56922-2ef2-4bc5-aa32-45cc9862b79e)

Qt版本设置：

在菜单栏点击“扩展” —— “Qt VS Tools” —— “Qt Versions”，在弹出的界面中配置Qt的编译器版本，先点击“Path”在弹出的对话框中选择Qt编译器的路径，再设置前面的“Version”，设定好之后点击“确定”。

![image](https://github.com/Open3DV/Xema/assets/117330523/bdfc5143-52b6-4e97-a63d-8270479919c5)

![image](https://github.com/Open3DV/Xema/assets/117330523/9b19c42c-ad35-4e5e-848f-6b3934e6de75)

编译执行：

在VS2019解决方案界面，右键点击“生成解决方案”开始编译；

![image](https://github.com/Open3DV/Xema/assets/117330523/692d23ae-df85-4174-a66e-c1752ac555f1)

生成的文件release：

VS编译完成后，在xema\x64\Release目录下，双击open_cam3d_gui.exe打开并使用xema_gui（具体软件的使用可以参考《XEMA系列相机使用手册》）
 
![image](https://github.com/Open3DV/Xema/assets/117330523/87c7f8c3-0603-48ef-bb76-3485d9ab0def)

### 2.ConfiguringIP 编译（相机搜索工具）

下载源代码，PC任意选这个一个路径地址，打开终端执行：

git clone https://gitee.com/open3dv/ConfiguringIP.git

双击ConfiguringIP.sln打开进行编译，过程与xema的配置过程完全一致。

生成的文件：

![image](https://github.com/Open3DV/Xema/assets/117330523/d53ac2e6-15bc-447d-b440-78f1877c7356)


因执行同样要依赖Qt的动态库，所以需要将xema\x64\Release中的platforms文件夹拷贝到ConfiguringIP\x64\Release中；

然后双击configuring_network_gui.exe打开IP搜索配置gui；

也可将configuring_ip.exe和configuring_network_gui.exe拷贝至xema编译之后的Release文件夹内，再运行操作。

## 五、相机标定

### 1，光机/相机调焦

1)光圈设置：

a)根据相机工作距离，将相机固定，准备好相应规格的标定板；打开相机的外盖，调节光圈：xema-L：F2.8，xema-S：F6.5，xema-D：F6.5，xema-P：F4.0
（以上为官方标准光圈值，用户也可根据自身需求自定义变更）

2)调焦：

a)对内部的光机和相机进行调焦，使其在标定距离处对焦清晰；

![image](https://github.com/Open3DV/Xema/assets/117330523/5eb4269e-969f-40ac-8d16-160bafd9ef23)

b)进入编译后的xema/X64/Release文件夹，终端运行./open_cam3d.exe；

![image](https://github.com/Open3DV/Xema/assets/117330523/afa45371-ae28-411b-8310-2c23c630bc59)

c)相机投影范围内垫满白纸，终端执行如下指令对光机和相机进行调焦；

![image](https://github.com/Open3DV/Xema/assets/117330523/8992df44-93ee-4ced-ac38-99fb4515d2be)

d)光机调焦清晰标准：使其投影在边缘以及中心的棋盘格内部的小棋盘格清晰可见；

![image](https://github.com/Open3DV/Xema/assets/117330523/ee38d0b0-62c3-496f-8cb4-c3e413ad2036)

e)相机调焦清晰标准：保证投影中心区域黑白棋盘格清晰可见情况下整体清晰度均匀

![image](https://github.com/Open3DV/Xema/assets/117330523/38ec4669-9d07-41fc-9c4e-fa816469fbaa)

### 2，采图标定

标定要拍摄N组图片，使用上位机软件open_cam3d.exe拍照获取，xema/X64/Release文件夹，终端运行./open_cam3d.exe，找到采图指令（如下图红框指示）：

![image](https://github.com/Open3DV/Xema/assets/117330523/3c478a47-58fe-4999-a9cb-2783dd93121a)

3)将标定板放置在距离相机适当的位置（取决于工作距离），执行拍照命令，获取一组图片（IP地址需要改为标定相机的IP地址）:

./open_cam3d.exe --get-raw-02 --ip 192.168.x.x --path .\capture\00

“.\capture\00”表示当前目录下capture文件夹内00组，Path对应路径可自定义更改


![image](https://github.com/Open3DV/Xema/assets/117330523/046b06bb-942d-4155-bd7a-798a7c68bb20)

4)在目标工作距离的约正负15%的范围内，变换标定板位姿，运行拍照命令，获取第二组图片：

![image](https://github.com/Open3DV/Xema/assets/117330523/8880b71e-8ba5-4041-9b20-b7bde3330b69)


./open_cam3d.exe --get-raw-02 --ip 192.168.x.x --path .\capture\01

接着重复以上操作，得到至少00~24组拍摄的图片，如需要获取00-24组共25张图片，则可以分五个位置（中心和四个角共五个位置）每个位置5张不同位姿进行拍摄。

![image](https://github.com/Open3DV/Xema/assets/117330523/01803f21-cdba-461f-9f94-f10925e5ea1f)


5)运行标定程序自动进行相机标定（这里需要注意标定板的规格设置），标定完成后，会在当前目录下生成标定参数文件param.txt：

.\calibration.exe --calibrate --use patterns --path ./capture/ --version 3010 --board 20 --calib ./param.txt

3010为光机型号，“board 20”表示标定板规则为20mm；具体根据实际情况变更即可

6)运行命令将标定结果写进相机：

.\open_cam3d.exe --set-calib-looktable --ip 192.168.x.x --path ./param.txt
至此：整个标定过程完成，GUI连接相机：查询标定参数是否匹配、深度图和高度图是否正确、采图保存点云是否正常





修订记录| | |
--|--|--
V0.5 | 2022.11.3 | 整理已有文档，并补充完善
V0.6 | 2022.11.5 | 完善软件安装部分
V0.7 | 2022.11.22 | 补充客户端软件编译部分
V1.1.0 | 2023.5.9 | 各个环节修改
V1.3.0 | 2023.7.3 | Nano系统安装补充完善
V1.4.0 | 2023.8.25 | 完善软件安装和标定步骤
V1.5.1 |2023.10.29|各环节图示及各步骤更新  
  |   |  
  |   |  
  |   |  
