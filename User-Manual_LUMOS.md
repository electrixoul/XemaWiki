# LUMOS振镜相机软件使用手册

![image](https://github.com/Open3DV/Xema/assets/117330523/f0c893c9-8644-4815-b585-dbad49942b0a)

Author:YaoHaihang&Caoyinyao

2023.10.8

## 一、产品简介
 
基于mems振镜的双目结构光3D相机嵌入式软件是基于mems振镜投影的结构光3D相机软件。基于核心硬件Ainstec mems芯片，Sony成像芯片和Nvidia Jetson Nano运算模块。数据传输使用GigE接口，支持多种曝光模式。本软件适用于3D扫描、工业3D缺陷检测，可配合工业机器人使用在工业无序抓取、上下料等使用场景。

![image](https://github.com/Open3DV/Xema/assets/117330523/b193e8a4-87d1-4c53-8e18-c7bcd1f0c523)

## 二、产品硬件展示

![image](https://github.com/Open3DV/Xema/assets/117330523/d9063171-3ee9-48b0-a3ec-4ac3adb6c33c)

## 三、硬件性能描述

![image](https://github.com/Open3DV/Xema/assets/117330523/ede29609-727e-4bf7-a9c5-d875021c083e)

## 四、硬件产品安装说明

### 1. 产品配件

![image](https://github.com/Open3DV/Xema/assets/117330523/c8e45778-cbab-4873-a983-0154ff2f808f)

### 2. 硬件连接

电脑通过网络访问相机有两种连接方式，一种是通过路由器连接进行交互，一种是通过网线直接连接进行通信。

当网络中不存在DHCP服务器时（即相机与电脑直连），相机的DHCP机制尝试30秒仍没有获取到IP，即转为AVAHI机制协商IP，协商出的IP在169.254.x.x网段，可通过SDK软件包中的configuring_network_gui.exe查看IP地址，具体说明将在下一节介绍。

相机上电前，首先确认电源线与网线连接牢靠，接通电源后“Power”指示灯常亮，约30秒钟相机启动完成，此时相机的网口绿色指示灯常亮、橙色指示灯闪烁，表明网络带宽为千兆。相机的“Act”工作指示灯在拍照及数据传输时点亮，平时为熄灭状态。

![image](https://github.com/Open3DV/Xema/assets/117330523/1d7730d8-9280-4e18-9324-bdab9a18aa21)

![image](https://github.com/Open3DV/Xema/assets/117330523/009e0cbe-444f-4569-8158-cffdcd11e74c)

### 3. 软件界面

打开界面后，输入configuring_network_gui.exe搜索到的IP地址，将其填地址栏内，并点击地址栏上方的连接按钮，连接相机以便进行后续操作

![image](https://github.com/Open3DV/Xema/assets/117330523/b1a7182a-de78-4711-9b87-607c149ccb4c)

点击红色框内的拍照图标，相机拍摄并在右侧显示所拍图像，可以选择显示框右上方的亮度图/深度图/高度图分别查看。为得到最佳有效的图像数据，投影亮度和曝光时间可在左侧的设置栏修改。点击拍照右侧的保存按钮，可以将拍摄的亮度图、点云图等保存至电脑，也可以勾选自动保存，拍摄后自动存储图片。
除以上设置，界面还提供了增益、置信度、平滑等参数供配置使用。


## 五、使用说明

### 1、高动态（HDR：范围：2~6 ）

高动态范围成像（英语：High Dynamic Range Imaging，[简称](https://baike.baidu.com/item/%E7%AE%80%E7%A7%B0/10492947?fromModule=lemma_inlink)HDRI或HDR），用来实现比普通数位图像技术更大曝光[动态范围](https://baike.baidu.com/item/%E5%8A%A8%E6%80%81%E8%8C%83%E5%9B%B4/6327032?fromModule=lemma_inlink)（即更大的明暗差别）的技术。

效果：高动态会使图片层次更分明，明暗差别明显。

使用方法：使用高动态时，可设置曝光的数量，对物体进行多次曝光。

![image](https://github.com/Open3DV/Xema/assets/117330523/35370cdb-24f5-415f-ac30-8ba62664aaf2)

高动态曝光数：HDR的次数，配合高动态模式使用。当高动态打开时，可选择高动态模式下需要曝光的次数，范围2-6，需要高动态模式时，请观察图片采集后效果选择曝光次数。

注意：默认高动态组数是2组，建议在满足点云质量的情况下使用更少的组数。在典型实例3中，将会介绍高动态的具体使用方法。

### 2、曝光时间（范围：2700~100000）

![image](https://github.com/Open3DV/Xema/assets/117330523/55eeae9a-63bb-45d2-8120-5c1b3116ab2e)

相机曝光时间：曝光时间是景物的反射光线通过镜头到达成像感光材料上，快门所打开的时间，简单解释就是在相机的快门打开的时候光线进入相机的时间。
实际使用过程根据物件特性调节曝光时间到最佳值。

### 3、过曝显示

曝光时间越长，进入的光线越多。曝光时间过长则会出现过曝的现象。对于过曝的查看：打开过曝显示开关，亮度图中显示红色的部分为过曝区域。

![image](https://github.com/Open3DV/Xema/assets/117330523/3f7da212-7ac5-4a1e-a35f-47bafcea3b91)

![image](https://github.com/Open3DV/Xema/assets/117330523/00b8b440-2d1a-4d93-9b6f-103a9208e834)

### 4、置信度（范围：0.0~100.0）

![image](https://github.com/Open3DV/Xema/assets/117330523/45ffb72f-c5aa-4ad0-9cd4-696191c33588)

置信度调低之后，黑色部分的深度信息（深度图）会被保留；相反，置信度调高之后黑色噪声会被去除；

![image](https://github.com/Open3DV/Xema/assets/117330523/57f33794-83b9-44a5-80e3-d56c3df24524)

![image](https://github.com/Open3DV/Xema/assets/117330523/32c13cba-091e-442e-9216-e6d923b5b901)

### 5、基准平面参数

高度映射基准平面：基准平面是在基准零位的一个平面,以拍摄的物体（如标定板）作为基准零位。若已知标定板的X、Y，根据右手定则可判断Z轴方向，标定板为基准平面，标定板正面为Z负方向（靠近相机），标定板反面则为Z正方向（远离相机）。

![image](https://github.com/Open3DV/Xema/assets/117330523/c3a2ec41-5819-4856-b3e7-9b6f252cb13c)

基准平面参数是数据测得，不可修改。如：

![image](https://github.com/Open3DV/Xema/assets/117330523/e2968ac1-9d8e-4151-85ca-017c4f66bacd)

![image](https://github.com/Open3DV/Xema/assets/117330523/4a587ed0-c3ac-4088-93f9-2c8b7c1227c2)

![image](https://github.com/Open3DV/Xema/assets/117330523/7077b3fd-7680-426f-b875-fa1c456d4409)

### 6、最大高度最小高度

![image](https://github.com/Open3DV/Xema/assets/117330523/7fd6d0ae-7a66-4636-bff9-88207c8b3b81)

最大高度（最大值）：9999.99 最小高度（最小值）：-9999

如果想利用高度图只想查看想观察的物体，这时可调节最大高度、最小高度，我们已知标定板（板定板可自行用其他物代替）为基准平面，则靠近相机为负，远离相机为正。

![image](https://github.com/Open3DV/Xema/assets/117330523/2c5aee08-52a0-437f-bcf0-dc6e2d83496e)

如：只想显示选择的金属工件，则只需要将最大高度设置为0mm以下，如本次设置-1mm（紧贴基准平面），最小高度要等于或超过工件的长度，如本次设置-600mm。效果则是将工件以外的场景全部不显示，只保留工件的高度图。如图：

![image](https://github.com/Open3DV/Xema/assets/117330523/699c8dec-7ea2-466f-a6ec-0a16166d57aa)

### 7、增益  

![image](https://github.com/Open3DV/Xema/assets/117330523/bbab6504-44df-47de-9844-f15c88e504f0)

范围：0-24

增益：调节画面的亮暗，不建议设置。

### 8、半径滤波

![image](https://github.com/Open3DV/Xema/assets/117330523/afd68f69-0452-4d10-a4d2-23c7f96fff86)

半径范围：0-99.99，有效点范围：0-99

对于点云中的每一个点，确定一个半径为r的球体，选取有效点数，若内部点数小于有效点时，则认为是噪声点，应剔除。

### 9、深度滤波

![image](https://github.com/Open3DV/Xema/assets/117330523/2207c07b-a9fe-416a-aa19-d2a9fadf16df)

基于深度图的滤波方法，勾选为真作用否则禁用，在1000mm的距离下建议阈值为33。

### 10、标定板型号

型号选择：4mm/12mm/20mm/40mm/80mm

![image](https://github.com/Open3DV/Xema/assets/117330523/47a65e09-2397-4717-9a6d-df01ac881752)

### 11、相机IP地址：***.***.***.***

![image](https://github.com/Open3DV/Xema/assets/117330523/284d7780-23c8-4b8f-9a4f-dde931edfc54)

### 12、亮度Gamma

![image](https://github.com/Open3DV/Xema/assets/117330523/8bb2e4e9-3de7-4943-bf15-f4cd46aef00a)

当图像亮度不均匀时可以将gamma设置为小于1的数，会降低图像的对比度，但是会获得更好的暗部细节。

### 13、图标

![image](https://github.com/Open3DV/Xema/assets/117330523/98bf48c0-b1ff-4b01-8b21-ebae4fdfc348)

## 六、典型实例介绍：

本节以普通物体、黑色物体、金属镜面反光工件的顺序，由浅入深的讲解如何拍出一副清晰完整的点云图片。但参数不是绝对的，可视工作环境进行微调。

注：本节的点云图片都是在CloudCompare中查看的。

### 1、普通物体

在拍摄普通物体时，在不过曝的情况下，我们要尽量增加投影亮度和曝光时间，此时的拍摄效果将会达到最佳，具体参数值可根据现场调整。

![image](https://github.com/Open3DV/Xema/assets/117330523/ee734c57-e147-46ca-aa3a-1894c55a13d1)

![image](https://github.com/Open3DV/Xema/assets/117330523/9971b34e-6515-4ea2-846f-d946e939c0d8)

最终点云效果如图：

![image](https://github.com/Open3DV/Xema/assets/117330523/4291df53-a9df-4831-8651-160e765f34ab)

同时SDK支持拍摄彩色点云，效果如下：

![image](https://github.com/Open3DV/Xema/assets/117330523/a14115c1-05cd-4bf8-b169-f8c7d18089a0)

### 2、黑色物体

拍摄黑色物体，如空调压缩机

首先将投影亮度设置最大1023，曝光时间设置为69000，如果画面不够亮，也可在不过曝的情况下，增加曝光时间。如图所示

![image](https://github.com/Open3DV/Xema/assets/117330523/b2b5a6e2-0b5c-4186-b711-9a732f34167c)

![image](https://github.com/Open3DV/Xema/assets/117330523/652f6c29-be73-47a8-a4ef-b812d56c822f)

提高黑色物体尽可能完整点云信息，可增加曝光时间。如图所示：

![image](https://github.com/Open3DV/Xema/assets/117330523/e97bf285-ed50-4641-ba9a-c70a1b668257)

最后点云效果：

![image](https://github.com/Open3DV/Xema/assets/117330523/12f42806-e1d9-4494-b020-4990ed942936)

### 3、金属镜面反光工件（高动态）

![image](https://github.com/Open3DV/Xema/assets/117330523/70de6647-2159-46a9-af23-246d30497ed1)

实际场景中，当检测金属、铝箔表面、反光膜片、光滑表面的物品时，镜面反射会造成局部反射光过强，从而失去物体原有信息，这时候可通过高动态模式尽量将物件完整信息采集出来。

在实际操作环境中，根据物体的层次可选择高动态曝光数，如下实例：

第一步：我们要得到最亮处的深度信息，如设置曝光时间为10000，（置信度为5，噪点过滤为50），作为一组高动态下的曝光数据，不打开高动态情况下在高度图中，如图所示：

![image](https://github.com/Open3DV/Xema/assets/117330523/0b457475-436a-4ea9-9ced-f06205935c2b)

第二步：曝光时间为30000，（置信度为5）可作为一组高动态下的曝光数据，不打开高动态情况下在高度图中，如图所示。

![image](https://github.com/Open3DV/Xema/assets/117330523/5d0324a7-1ce2-4c16-a26a-ea4ae8b6968b)

第三步：开启高动态，曝光数设置为2，第一组数据：10000，1023；第二组数据：50000，1023。置信度5，如下图：

![image](https://github.com/Open3DV/Xema/assets/117330523/7e01dccd-0fea-43fc-a0ca-dbed5ec11649)

如图所示可得到清晰完整的一幅点云图片，无缺失。

![image](https://github.com/Open3DV/Xema/assets/117330523/62fb7794-c5e6-41d5-aeae-166a499f3d26)
