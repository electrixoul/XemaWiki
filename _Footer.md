# XEMA系列相机使用手册
## V1.0.6
![image](https://user-images.githubusercontent.com/117330523/221107297-6b9ca693-f00b-4153-aa30-9825d570cf3b.png)

目录

## 一、产品简介
	
## 二、产品展示
	
三、性能描述
	
四、产品安装说明
	
1. 产品配件
	
2. 硬件连接
	
3. 软件界面
	
五、使用说明	

1、高动态
	
2、相机曝光时间
	
3、投影亮度
	
4、过曝显示
	
5、置信度
	
6、噪点过滤
	
7、生成亮度图
	
8、基准平面参数
	
9、最大高度最小高度
	
10、增益 

11、半径滤波
	
12、标定板型号
	
13、相机IP地址
	
14、重复数
	
15、图标
	
六、典型实例介绍
	
1、普通物体
	
2、黑色物体
	
3、金属镜面反光工件	

一、产品简介

XEMA系列相机是基于DLP投影的结构光3D相机。核心部件采用TI DLP3010投影芯片，Sony IMX174成像芯片和Nvidia Jetson Nano运算模块。数据传输使用GigE接口，支持多种曝光模式。适用于3D扫描、工业3D缺陷检测，可配合工业机器人使用在工业无序抓取、上下料等使用场景。

二、产品展示

![image](https://user-images.githubusercontent.com/117330523/221108634-7b2fc049-e4ee-4021-8157-1944ae464573.png)

![image](https://user-images.githubusercontent.com/117330523/221108658-a4abc334-195b-432e-bc82-19660c50cd04.png)


三、性能描述

参数 | 值
-- | --
标定精度 | 0.05mm
点云分辨率 | 1920x1200
图像分辨率 | 1920x1200
帧率 | 1fps
基线长度 | 150mm
工作距离 | 400 ~ 2000mm
数据接口 | Ethernet
水平视角 | 40°
垂直视角 | 23°
外观尺寸 | 207 x 128 x 50.5 mm
重量 | 1000g
CPU | Quad-core Arm A57 processor @ 1.43 GHz
GPU | 128-core Maxwell GPU
内存 | 4GB 64-bit LPDDR4

四、产品安装说明

1. 产品配件

![image](https://user-images.githubusercontent.com/117330523/221108940-0a39d0da-d209-4bf4-9555-6c094c6bf0a1.png)


2. 硬件连接

电脑通过网络访问相机有两种连接方式，一种是通过路由器连接进行交互，一种是通过网线直接连接进行通信。

![image](https://user-images.githubusercontent.com/117330523/221109043-66d15dd9-9799-4b93-afba-92b1081ad53c.png)


![image](https://user-images.githubusercontent.com/117330523/221109081-28d42238-8ec1-4cfd-bdcb-f699978633c0.png)


当网络中不存在DHCP服务器时（即相机与电脑直连），相机的DHCP机制尝试30秒仍没有获取到IP，即转为AVAHI机制协商IP，协商出的IP在169.254.x.x网段，可通过SDK软件包中的configuring_network_gui.exe查看IP地址，具体说明将在下一节介绍。

![image](https://user-images.githubusercontent.com/117330523/221109126-f6d25257-64c9-4784-9b2a-cad22af45ea6.png)


相机上电前，首先确认电源线与网线连接牢靠，接通电源后“Power”指示灯常亮，约30秒钟相机启动完成，此时相机的网口绿色指示灯常亮、橙色指示灯闪烁，表明网络带宽为千兆。相机的“Act”工作指示灯在拍照及数据传输时点亮，平时为熄灭状态。

3. 软件界面

1)ConfiguringIP界面介绍
打开configuring_network_gui.exe，点击搜索相机，显示界面如下图所示：

![image](https://user-images.githubusercontent.com/117330523/221109220-b0980fff-24a2-4e44-a0a0-2f394c9690a4.png)

搜索到的相机会列表显示，左列为该相机的MAC地址，右列即为相机IP，前面讲到的相机与电脑直连时，开机后搜索到的协商IP地址类似下图。

![image](https://user-images.githubusercontent.com/117330523/221109308-6dad0546-845a-48b9-9cd7-c8d1afbc86ce.png)


2)OpenCam3D界面介绍

![image](https://user-images.githubusercontent.com/117330523/221110851-0465e352-1b44-47eb-9c08-7f97aa1ea58f.png)

打开界面后，输入上一节搜索到的IP地址，将其填入红色地址栏内，并点击地址栏上方的连接按钮，连接相机以便进行后续操作，如果连接成功，界面左下方的信息栏会提示连接成功。

![image](https://user-images.githubusercontent.com/117330523/221110898-632ffd55-d675-4522-9dc3-5d3ab25fab53.png)

点击红色框内的拍照图标，相机拍摄并在右侧显示所拍图像，可以选择显示框右上方的亮度图/深度图/高度图分别查看。为得到最佳有效的图像数据，投影亮度和曝光时间可在左侧的设置栏修改。点击拍照右侧的保存按钮，可以将拍摄的亮度图、点云图等保存至电脑，也可以勾选自动保存，拍摄后自动存储图片。
除以上设置，界面还提供了增益、置信度、平滑、重复拍摄次数等参数供配置使用。

五、使用说明

1、高动态（HDR）
（可设置曝光数量）

高动态范围成像（英语：High Dynamic Range Imaging，[简称](https://baike.baidu.com/item/%E7%AE%80%E7%A7%B0/10492947?fromModule=lemma_inlink)HDRI或HDR），用来实现比普通数位图像技术更大曝光[动态范围](https://baike.baidu.com/item/%E5%8A%A8%E6%80%81%E8%8C%83%E5%9B%B4/6327032?fromModule=lemma_inlink)（即更大的明暗差别）的一组技术。

效果：高动态会使图片层次更分明，明暗差别明显。

使用方法：使用高动态时，可设置曝光的数量，对物体进行多次曝光。

曝光数量 
 
![image](https://user-images.githubusercontent.com/117330523/221111092-e4a972e2-d01b-4997-958e-ae2e4db86974.png)

范围：1-6 

曝光数量：曝光的次数，配合高动态使用。当高动态打开时，可选择高动态模式下需要曝光的次数，范围1-6，需要高动态模式时，请观察图片选择曝光次数。高动态模式下，曝光时间和投影亮度为一组

注意：默认高动态组数是2组，建议在满足点云质量的情况下使用更少的组数。在典型实例3中，将会介绍高动态的具体使用方法。

组数（数据可修改）：

当组数为1，曝光参数（曝光时间）为6000，亮度参数（投影亮度）为1023；

当组数为2，曝光参数（曝光时间）为12000，亮度参数（投影亮度）为1023；

当组数为3，曝光参数（曝光时间）为24000，亮度参数（投影亮度）为1023；

当组数为4，曝光参数（曝光时间）为36000，亮度参数（投影亮度）为1023；

当组数为5，曝光参数（曝光时间）为48000，亮度参数（投影亮度）为1023；

当组数为6，曝光参数（曝光时间）为60000，亮度参数（投影亮度）为1023；

![image](https://user-images.githubusercontent.com/117330523/221111215-ca8f14a2-94cb-4f51-b0f7-3c2c58888ae4.png)

![image](https://user-images.githubusercontent.com/117330523/221111252-e68c3313-d7e2-4b52-828b-17f1129bef54.png)


2、相机曝光时间

![image](https://user-images.githubusercontent.com/117330523/221111293-ae85bbfd-2588-476c-893e-2f5be2a29d4e.png)

范围：1700-100000

相机曝光时间：曝光时间是景物的反射光线通过镜头到达成像感光材料上，快门所要打开的时间。简单解释就是在相机的快门打开的时候光线进入相机的时间。
曝光时间越长，进入的光线越多。曝光时间过长则会出现过曝的现象。对于过曝的查看：打开过曝显示开关，亮度图中显示红色的部分为过曝区域。

![image](https://user-images.githubusercontent.com/117330523/221111331-19c6fa0d-5f13-42a5-a99a-2568e96c2b7c.png)

![image](https://user-images.githubusercontent.com/117330523/221111354-371b73e7-2b2f-4b73-a48c-b06d6b189ad5.png)


3、投影亮度

![image](https://user-images.githubusercontent.com/117330523/221111387-d675c896-8c9d-4390-8998-2986a7a92f02.png)

范围：0-1023

注意：优先使用最大亮度1023

投影亮度：投影亮度就是指投影光线的强度，光线强度越大，图像就越明亮、越清晰，在一定范围内，人眼会因为亮度大而觉得画面更清晰，如果超过这个限度，过强的亮度则会导致无法看清图像。

![image](https://user-images.githubusercontent.com/117330523/221111559-5f974ef2-08fa-4acf-a64d-1d79209cb4bd.png)

![image](https://user-images.githubusercontent.com/117330523/221111653-2bdda4e1-88c7-43f2-aec0-b618a3e874db.png)


4、过曝显示

在进行拍摄时，难免会出现过曝的现象，在亮度图中，勾选过曝按钮就可观察过曝的区域，这样就可以改变相关的参数，如曝光时间、亮度、HDR模式等操作进行矫正。

![image](https://user-images.githubusercontent.com/117330523/221111816-fd01d796-628d-46c5-a8f9-214c8b4bba22.png)

![image](https://user-images.githubusercontent.com/117330523/221111866-0ed8a324-1ec9-4451-bd45-688d976bbb20.png)

5、置信度

![image](https://user-images.githubusercontent.com/117330523/221111992-cfeb83e0-b40f-47be-97c6-9aedf895f803.png)

范围：0-100

置信度调低之后，黑色部分的深度信息（深度图）会被保留；

![image](https://user-images.githubusercontent.com/117330523/221112056-307a6334-d371-4c35-b35a-91bc5be9c9d5.png)

相反，置信度调高之后黑色噪声会被去除。

![image](https://user-images.githubusercontent.com/117330523/221112100-0fc87765-55f5-4a84-86f7-0da815ad85a4.png)


6、噪点过滤

![image](https://user-images.githubusercontent.com/117330523/221112133-0afb299d-84ca-490c-8977-3bea51c17824.png)

范围0-100

在机器视觉应用场景中,如检测金属、铝箔表面、反光膜片、光滑表面的物品时,镜面反射会造成局部反射光过强,从而失去物体原有信息,干扰机器视觉检测。噪点过滤可将产生的噪声部分消除，保存物体原有信息。

![image](https://user-images.githubusercontent.com/117330523/221112212-2cd23513-6351-47bf-af97-4ee7fcf174f0.png)

![image](https://user-images.githubusercontent.com/117330523/221112227-c900367b-f2ab-4b55-bad7-7f9242179729.png)



7、生成亮度图

生成亮度图在界面最底端。

有三种模式：默认、自定义发光、自定义不发光。
一般是默认模式。

自定义发光则可以自行设置曝光时间。

自定义不发光则是环境中的光线亮度。

![image](https://user-images.githubusercontent.com/117330523/221112298-2375dfa3-f85d-49ce-abd6-d80778ef3599.png)

 
8、基准平面参数

高度映射基准平面：基准平面是在基准零位的一个平面,以拍摄的物体（如标定板）作为基准零位。若已知标定板的X、Y，根据右手定则可判断Z轴方向，标定板为基准平面，标定板正面为Z负方向（靠近相机），标定板反面则为Z正方向（远离相机）。

![image](https://user-images.githubusercontent.com/117330523/221112330-4af22423-65a1-4001-af3c-6237b525d5bc.png)


基准平面参数是数据测得，不可修改。
如：

![image](https://user-images.githubusercontent.com/117330523/221112364-8975412f-a3ae-4bc5-b635-54a389fa6713.png)

![image](https://user-images.githubusercontent.com/117330523/221112399-cd821277-a0f6-4a9e-ad0b-2a2871914969.png)

![image](https://user-images.githubusercontent.com/117330523/221112432-099f0455-c197-40fd-84e5-8467035299dd.png)


    

  







9、最大高度最小高度

![image](https://user-images.githubusercontent.com/117330523/221112487-0696298e-3207-457c-bdb8-8498f47f3ff7.png)

最大高度（最大值）：9999.99 最小高度（最小值）：-9999

如果想利用高度图只想查看想观察的物体，这时可调节最大高度、最小高度，我们已知标定板（板定板可自行用其他物代替）为基准平面，则靠近相机为负，远离相机为正。

![image](https://user-images.githubusercontent.com/117330523/221112518-a6fb351c-1334-472c-aba0-8537ea6fc12d.png)


如：只想显示选择的金属工件，则只需要将最大高度设置为0mm以下，如本次设置-1mm（紧贴基准平面），最小高度要等于或超过工件的长度，如本次设置-600mm。效果则是将工件以外的场景全部不显示，只保留工件的高度图。如图：

![image](https://user-images.githubusercontent.com/117330523/221112571-4d0e8f4f-632e-47a5-b990-af3577971942.png)


10、增益  

![image](https://user-images.githubusercontent.com/117330523/221112598-a1046e8c-1c36-4833-a921-393d523a9100.png)

  
范围：0-10

增益：调节画面的亮暗，不建议设置。

11、半径滤波

![image](https://user-images.githubusercontent.com/117330523/221112626-2c944e13-15ae-4d17-9f57-23ff9f7c92ef.png)

![image](https://user-images.githubusercontent.com/117330523/221112644-5448cfea-3a55-4cd1-aa59-93adf124e25d.png)



半径范围：0-99.99）

有效点范围：0-99

对于点云中的每一个点，确定一个半径为r的球体，选取有效点数，若内部点数小于有效点时，则认为是噪声点，应剔除。

12、标定板型号

型号选择：4mm/12mm/20mm/40mm/80mm

![image](https://user-images.githubusercontent.com/117330523/221112706-59f7e9e0-037e-4a97-b2e0-59413d32e605.png)

![image](https://user-images.githubusercontent.com/117330523/221112727-3c62f155-847e-4ed2-a2c6-6a8d08d7df18.png)


13、相机IP地址：***.***.***.***

![image](https://user-images.githubusercontent.com/117330523/221112769-6535109f-1f55-4f7f-a79d-44803157214a.png)


14、重复数

![image](https://user-images.githubusercontent.com/117330523/221112816-0254b815-488f-4c6e-9a7a-4ad12d0c4872.png)

范围：0-10

相机要重复拍摄的次数，作用是提高信噪比（信号与噪声的比例），信噪比越高越好，这样随机噪声将会被抑制，增加了有效信息。




15、图标

  | GUI图标
-- | --
  | 连续拍摄开始图标
  | 连续拍摄停止图标
  | 连接相机
  | 保存按钮
  | 打开文件夹
  | 获得相机标定参数（内参、外参、畸变、基准平面参数）
  | 连接相机图标
  | 单次拍摄图标
  | 获得相机精度图标

六、典型实例介绍：

本节以普通物体、黑色物体、金属镜面反光工件的顺序着手，由浅入深的讲解如何拍出一副清晰完整的点云图片。但参数不是绝对的，可视工作环境进行微调。

注：本节的点云图片都是在CloudCompare中查看的。

1、普通物体

在拍摄普通物体时，在不过曝的情况下，我们要尽量增加投影亮度和曝光时间，此时的拍摄效果将会达到最佳。

首先设置投影亮度最高1023，曝光时间最小20000，置信度为10保留深度信息，这时在亮度图中没有发现过曝现象。但是高度图标注的部分黑色区域没有显示（拍摄的猫咪耳朵位置）。

![image](https://user-images.githubusercontent.com/117330523/221113181-9139c489-599f-4e0b-9ae0-f771950d061f.png)

这时可增加重复数，增加有效信息，例如设置为6，如果亮度图此时稍暗，可适当增加曝光时间，如这里从20000增加到22000，再增加将会过曝，应注意！

![image](https://user-images.githubusercontent.com/117330523/221113244-f93ec388-3046-41a1-b6c6-7fb1167fe982.png)

最终效果如图：

![image](https://user-images.githubusercontent.com/117330523/221113262-6894956e-22da-4493-817e-1105e419c2d1.png)

2、黑色物体

拍摄黑色物体，如一块纯黑色的海绵。

首先将投影亮度设置最大1023，曝光时间设置为35000，如果画面不够亮，也可在不过曝的情况下，增加曝光时间。如图所示

![image](https://user-images.githubusercontent.com/117330523/221113319-f167e1a7-80fd-4a69-ba8f-b3d4d4b6872a.png)

![image](https://user-images.githubusercontent.com/117330523/221113341-516632b4-568b-4d69-8666-46ff772baa78.png)

但发现在高度图中海绵有很多的随机噪声，这时我们提高重复数为5，目的是提高信噪比，这样随机噪声将会被抑制，增加了有效信息。如图所示：

![image](https://user-images.githubusercontent.com/117330523/221113393-5d4c95b9-8f2e-4406-8704-4bfd90b281b8.png)

最后点云效果：

![image](https://user-images.githubusercontent.com/117330523/221113425-1b1576fc-018f-4e4e-aa5f-411ac832c8a3.png)

![image](https://user-images.githubusercontent.com/117330523/221113441-a477aa3d-5ad0-4b90-9c99-311034e079d8.png)




3、金属镜面反光工件（高动态）

![image](https://user-images.githubusercontent.com/117330523/221113466-a69c243c-7622-4004-bf29-b5db24467e44.png)

检测金属、铝箔表面、反光膜片、光滑表面的物品时,镜面反射会造成局部反射光过强,从而失去物体原有信息。

在实际操作环境中，根据物体的层次可选择曝光数，例如上图，有工件、黑色版、带孔平台，这时我们可选择曝光次数为3。

第一步：首先将投影亮度设置为最大1023，将曝光时间设置为30000，目的是能够得到最暗处的深度信息，（置信度为5，噪点过滤为50），这可作为一组高动态下的曝光数据，不打开高动态情况下在高度图中，如图所示，我们可以看到最外层黑色版的深度信息。

![image](https://user-images.githubusercontent.com/117330523/221113541-df04aea8-786d-443f-9364-729ac0bd22dc.png)

第二步：我们要得到最亮处的深度信息，将第一步中工件缺失部分（最亮）的深度信息显示出来。如降低投影亮度为1023，曝光时间为1700，（置信度为5，噪点过滤为50），这可作为一组高动态下的曝光数据，不打开高动态情况下在高度图中，如图所示，可见之前工件缺失（最亮部分）的信息成功显现。

![image](https://user-images.githubusercontent.com/117330523/221113582-9d809b66-f600-40d8-9671-c7aedb22ed06.png)

第三步：投影亮度设置个第一步和第二步的中间值为800，曝光时间为25000，（置信度为5，噪点过滤为50）可作为一组高动态下的曝光数据，不打开高动态情况下在高度图中，如图所示。

![image](https://user-images.githubusercontent.com/117330523/221113608-5550c352-4eaf-42b3-b6ca-4ac02942a3f8.png)

第四步:开启高动态，曝光数设置为3，第一组数据：1700，1023；第二组数据：30000,1023；第三组数据：25000，800。置信度5，噪点过滤50


![image](https://user-images.githubusercontent.com/117330523/221113633-b50d77bf-358c-4a20-a043-ad85adc46cc3.png)

如图所示可得到清晰完整的一幅点云图片，无缺失。

![image](https://user-images.githubusercontent.com/117330523/221113668-369ea6f1-8d22-41d7-88b8-11ba2d8834cf.png)
