# XEMA系列相机使用手册
## V1.5.0
## Author:YaoHaihang
## 2023.8.8
	

##  一、产品简介

  XEMA系列相机是基于DLP投影的结构光3D相机。核心部件采用TI DLP3010投影芯片，Sony IMX174成像芯片和Nvidia Jetson Nano运算模块。数据传输使用GigE接口，支持多种曝光模式。适用于3D扫描、工业3D缺陷检测，可配合工业机器人使用在工业无序抓取、上下料等使用场景。

##  二、产品展示

![image](https://user-images.githubusercontent.com/117330523/221108634-7b2fc049-e4ee-4021-8157-1944ae464573.png)

![image](https://github.com/Open3DV/Xema/assets/117330523/73d2f283-7c49-422c-a61f-8d255ca66244)

![image](https://github.com/Open3DV/Xema/assets/117330523/040b83aa-255c-4490-a80c-55e2c87ff8d7)



## 三、参数

![image](https://github.com/Open3DV/Xema/assets/117330523/89b375f1-5664-441b-9d75-58fe51d0a31d)

## 四、产品安装说明

### 1. 产品配件

![image](https://github.com/Open3DV/Xema/assets/117330523/5e77ed95-7025-4220-89d1-c8a9b35383a6)


### 2. 硬件连接

电脑通过网络访问相机有两种连接方式，一种是通过路由器连接进行交互，一种是通过网线直接连接进行通信。

![new1](https://user-images.githubusercontent.com/117330523/228769660-b823103c-1f9c-42e4-ae83-5b3a6cc42021.png)


![new2](https://user-images.githubusercontent.com/117330523/228769704-e63d2641-81a5-486f-a642-ebb5ef75189e.png)


当网络中不存在DHCP服务器时（即相机与电脑直连），相机的DHCP机制尝试30秒仍没有获取到IP，即转为AVAHI机制协商IP，协商出的IP在169.254.x.x网段，可通过SDK软件包中的configuring_network_gui.exe查看IP地址，具体说明将在下一节介绍。

相机上电前，首先确认电源线与网线连接牢靠，接通电源后“Power”指示灯常亮，约30秒钟相机启动完成，此时相机的网口绿色指示灯常亮、橙色指示灯闪烁，表明网络带宽为千兆。相机的“Act”工作指示灯在拍照及数据传输时点亮，平时为熄灭状态。

### 3. 软件界面

1)ConfiguringIP界面介绍
打开configuring_network_gui.exe，点击搜索相机，显示界面如下图所示：

![image](https://github.com/Open3DV/Xema/assets/117330523/f22e6b80-0ee5-4b4d-b240-b7f2038dd31e)

搜索到的相机会列表显示，左列为该相机的MAC地址，右列即为相机IP，前面讲到的相机与电脑直连时，开机后搜索到的协商IP地址类似下图。

![image](https://github.com/Open3DV/Xema/assets/117330523/4c703ecc-ffc1-444d-a709-b00d69ae03e2)


2)OpenCam3D界面介绍

![image](https://github.com/Open3DV/Xema/assets/117330523/89038634-c69e-4b9a-ae06-c5dc67dc55b0)

打开界面后，输入上一节搜索到的IP地址，将其填入红色地址栏内，并点击地址栏上方的连接按钮，连接相机以便进行后续操作，如果连接成功，界面左下方的信息栏会提示连接成功。

![image](https://github.com/Open3DV/Xema/assets/117330523/edd8ceff-4612-49c7-a304-4f5a225d20bb)

点击红色框内的拍照图标，相机拍摄并在右侧显示所拍图像，可以选择显示框右上方的亮度图/深度图/高度图分别查看。为得到最佳有效的图像数据，投影亮度和曝光时间可在左侧的设置栏修改。点击拍照右侧的保存按钮，可以将拍摄的亮度图、点云图等保存至电脑，也可以勾选自动保存，拍摄后自动存储图片。
除以上设置，界面还提供了增益、置信度、平滑、重复拍摄次数等参数供配置使用。

## 五、使用说明

### 1、高动态（HDR：范围：2~6 ）

高动态范围成像（英语：High Dynamic Range Imaging，[简称](https://baike.baidu.com/item/%E7%AE%80%E7%A7%B0/10492947?fromModule=lemma_inlink)HDRI或HDR），来实现比普通数位图像技术更大曝光[动态范围](https://baike.baidu.com/item/%E5%8A%A8%E6%80%81%E8%8C%83%E5%9B%B4/6327032?fromModule=lemma_inlink)（即更大的明暗差别）的一组技术。

效果：高动态会使图片层次更分明，明暗差别明显（特别是面对反光工件）。

使用方法：使用高动态时，可根据具体的场景和工件，选择需要的组数，范围2-6，曝光时间和投影亮度为一组；设置合适的曝光时间和投影亮度值对物体进行多次曝光来达到最佳的拍摄效果。

![image](https://github.com/Open3DV/Xema/assets/117330523/3c01c780-d533-45f6-8513-9becca65e121)

注意：默认高动态组数是 2 组，建议在满足点云质量的情况下使用更少的组数。 

在典型实例 3 中，将会介绍高动态的具体使用方法。

### 2、相机曝光时间

![image](https://github.com/Open3DV/Xema/assets/117330523/e40726ee-840a-43f1-84f6-424d55c21638)

范围：1700-100000

相机曝光时间：曝光时间是景物的反射光线通过镜头到达成像感光材料上，快门所要打开的时间。简单解释就是在相机的快门打开的时候光线进入相机的时间。
曝光时间越长，进入的光线越多。曝光时间过长则会出现过曝的现象。对于过曝的查看：打开过曝显示开关，亮度图中显示红色的部分为过曝区域。

![image](https://github.com/Open3DV/Xema/assets/117330523/6149f9e3-e79c-451e-8e27-c8fd1d6b6915)

![image](https://github.com/Open3DV/Xema/assets/117330523/974e40fe-6dcc-4d5f-9c98-01d0513af4df)


### 3、投影亮度

![image](https://github.com/Open3DV/Xema/assets/117330523/78d36ccf-1af0-4eb9-a3bd-cd3f4e0afea6)

范围：0-1023

注意：优先使用最大亮度1023

投影亮度：投影亮度就是指投影光线的强度，光线强度越大，图像就越明亮、越清晰，在一定范围内，人眼会因为亮度大而觉得画面更清晰，如果超过这个限度，过强的亮度则会导致无法看清图像。

![image](https://github.com/Open3DV/Xema/assets/117330523/8af795c5-7dc8-4579-a0e3-fdef4ea6a16b)

![image](https://github.com/Open3DV/Xema/assets/117330523/6494d0eb-96a9-44d8-bde2-67facc5ba774)


### 4、过曝显示

在进行拍摄时，难免会出现过曝的现象，在亮度图中，勾选过曝按钮就可观察过曝的区域，这样就可以改变相关的参数，如曝光时间、亮度、HDR模式等操作进行矫正。

![image](https://github.com/Open3DV/Xema/assets/117330523/c8a2349a-4d2a-4c5d-acdd-d46d43c91e2b)

![image](https://github.com/Open3DV/Xema/assets/117330523/59e3a275-2462-4feb-826d-185cbb430a4f)

### 5、置信度

![image](https://github.com/Open3DV/Xema/assets/117330523/87b88407-79f9-4c6f-ad71-3792ef052acd)

范围：0-100

置信度调低之后，黑色部分的深度信息（深度图）会被保留；相反，置信度调高之后黑色噪声会被去除。

![image](https://github.com/Open3DV/Xema/assets/117330523/16de7081-86d6-49f1-9a97-99ae9d3b9436)


![image](https://github.com/Open3DV/Xema/assets/117330523/f6a9c9df-24ce-4ee2-be84-21f39241d47c)


### 6、噪点过滤

![image](https://user-images.githubusercontent.com/117330523/221112133-0afb299d-84ca-490c-8977-3bea51c17824.png)

范围0-100

在机器视觉应用场景中,如检测金属、铝箔表面、反光膜片、光滑表面的物品时,镜面反射会造成局部反射光过强,从而失去物体原有信息,干扰机器视觉检测。噪点过滤可将产生的噪声部分消除，保存物体原有信息。

![image](https://github.com/Open3DV/Xema/assets/117330523/193dd91f-41a6-4060-aa0b-be88846f44c0)

![image](https://github.com/Open3DV/Xema/assets/117330523/2615db7f-c65e-4633-9dd5-16b97ceba0bf)



### 7、生成亮度图

将界面功能滑动条滑到最低端，找到生成亮度图功能区域。

有三种模式：默认、自定义发光、自定义不发光。一般是默认模式。

自定义发光则可以自行设置曝光时间、增益，拍摄方式（单曝光或高动态）。

自定义不发光则是环境中的光线亮度，也可自行设置曝光时间、增益，拍摄方式（单曝光或高动态）。

![image](https://github.com/Open3DV/Xema/assets/117330523/6363aa06-8351-4402-afb7-10bbfbb046b8)

![image](https://github.com/Open3DV/Xema/assets/117330523/6ded1d5e-bd34-4cfe-862e-bd516f4e3e4f)

 
### 8、基准平面参数

高度映射基准平面：基准平面是在基准零位的一个平面,以拍摄的物体（如标定板）作为基准零位。若已知标定板的X、Y，根据右手定则可判断Z轴方向，标定板为基准平面，标定板正面为Z负方向（靠近相机），标定板反面则为Z正方向（远离相机）。

![image](https://user-images.githubusercontent.com/117330523/221112330-4af22423-65a1-4001-af3c-6237b525d5bc.png)


基准平面参数是数据测得，不可修改。
如：

![image](https://user-images.githubusercontent.com/117330523/221116271-22d8ab52-2a8c-4c2f-b078-194419fee0af.png)

![image](https://github.com/Open3DV/Xema/assets/117330523/d3eb2e8a-b152-42d8-a705-ad2fde985233)

![image](https://user-images.githubusercontent.com/117330523/221112432-099f0455-c197-40fd-84e5-8467035299dd.png)


    

  







### 9、最大高度最小高度

![image](https://user-images.githubusercontent.com/117330523/221112487-0696298e-3207-457c-bdb8-8498f47f3ff7.png)

最大高度（最大值）：9999.99 最小高度（最小值）：-9999

如果想利用高度图只想查看想观察的物体，这时可调节最大高度、最小高度，我们已知标定板（板定板可自行用其他物代替）为基准平面，则靠近相机为负，远离相机为正。

![image](https://user-images.githubusercontent.com/117330523/221112518-a6fb351c-1334-472c-aba0-8537ea6fc12d.png)


如：只想显示选择的金属工件，则只需要将最大高度设置为0mm以下，如本次设置-1mm（紧贴基准平面），最小高度要等于或超过工件的长度，如本次设置-600mm。效果则是将工件以外的场景全部不显示，只保留工件的高度图。如图：

![image](https://github.com/Open3DV/Xema/assets/117330523/3c137689-e1e4-4620-9868-2c14a613b52d)


### 10、增益  

![image](https://user-images.githubusercontent.com/117330523/221112598-a1046e8c-1c36-4833-a921-393d523a9100.png)

  
范围：0-10

增益：调节画面的亮暗，不建议设置。

### 11、半径滤波

![image](https://github.com/Open3DV/Xema/assets/117330523/cf249702-99ee-4afe-9502-bfffe9c0c0cf)

![image](https://github.com/Open3DV/Xema/assets/117330523/aa8f78b5-37b8-4438-b0d9-06d1c1d3e1bf)



半径范围：0-99.99）

有效点范围：0-99

对于点云中的每一个点，确定一个半径为r的球体，选取有效点数，若内部点数小于有效点时，则认为是噪声点，应剔除。

### 12、深度滤波

![image](https://github.com/Open3DV/Xema/assets/117330523/907677d0-3315-4816-b306-e30bccd659cf)

基于深度图的滤波方法，勾选为真作用否则禁用，在1000mm的距离下建议阈值为33。

### 13、标定板型号

型号选择：4mm/12mm/20mm/40mm/80mm

![image](https://github.com/Open3DV/Xema/assets/117330523/398e2e7e-d801-4bec-b229-716d3750bfff)

![image](https://github.com/Open3DV/Xema/assets/117330523/bfcdb437-c8bc-45c3-b27b-a514bb97b81b)


### 14、相机IP地址：***.***.***.***

![image](https://user-images.githubusercontent.com/117330523/221112769-6535109f-1f55-4f7f-a79d-44803157214a.png)


### 15、重复数

![image](https://user-images.githubusercontent.com/117330523/221112816-0254b815-488f-4c6e-9a7a-4ad12d0c4872.png)

范围：0-10

相机要重复拍摄的次数，作用是提高信噪比（信号与噪声的比例），信噪比越高越好，这样随机噪声将会被抑制，增加了有效信息。

### 16、保存

![image](https://github.com/Open3DV/Xema/assets/117330523/512cd270-91e1-4b51-a348-624be0d9ca7c)ng)

点击保存按钮，可选择原图或去畸变进行保存，也可选择不再提示。

### 17、引擎

![image](https://github.com/Open3DV/Xema/assets/117330523/2a5967aa-5c23-40a6-b810-d976eb77c003)

在引擎中我们可以选择不同的引擎模式，包括常规模式和高反模式。高反模式则是应对高反光工件的特殊引擎，例如一个高反光工件在用常规模式的高动态时，效果依然不理想，这时便可使用高反模式，以下是一个拍摄高反光工件的例子。(对于旧相机，可能需要重新烧录条纹才支持高反模式）

![image](https://github.com/Open3DV/Xema/assets/117330523/66bc2e8f-7427-4c37-8c63-226439f48e37)

![image](https://github.com/Open3DV/Xema/assets/117330523/7f1c5d99-d5a3-4919-a025-be59e1347573)

上图中，可见常规模式的高动态模式下，工件部分深度信息和点云信息依旧缺失。在开启高反模式后，工件信息完整，如下图所示。

![image](https://github.com/Open3DV/Xema/assets/117330523/b64fa7c2-11c5-4381-a5c3-eb9dbe3b5aa8)

![image](https://github.com/Open3DV/Xema/assets/117330523/8c4830d6-c1ad-457e-97cd-7fe4bb4097e3)

### 18、相位校正

![image](https://github.com/Open3DV/Xema/assets/117330523/12228728-0030-4161-bd84-538d2bb28b18)

相位校正即点云灰度补偿，是一种在三维点云数据中对灰度信息进行校正的方法。 点云灰度补偿的目的是消除这些灰度值差异，并将点云中的灰度信息转化为与实际物体表面反射率相对应的数值。

![image](https://github.com/Open3DV/Xema/assets/117330523/b7a9ff32-d14e-4e49-bc0a-c50d440a01de)


应用步骤：首先放置标定板，点击基准平面校正按钮，以标定板的平面为基准平面。如上图所示。

![image](https://github.com/Open3DV/Xema/assets/117330523/0d0c9e1c-59ce-40cb-b5cc-dadc5db79c18)

如最大高度最小高度章节介绍，将最大高度调为1，最小高度调为-1，只显示标定板部分，如上图所示。

![image](https://github.com/Open3DV/Xema/assets/117330523/e5697c86-caf2-474d-aac0-99e179be251f)


在不打开相位校正时，标定板如上图所示，在实际的标定板中整个是平面，圆和非圆部分不存在上下起伏，但实际拍出的效果则是圆有起伏。

![image](https://github.com/Open3DV/Xema/assets/117330523/d1196d44-450b-4023-89d7-6bcd0ad65d20)

在打开相位校正后，发现标定板基本不存在颜色差异或差异不明显，说明校正成功。

### 19、关于

![image](https://github.com/Open3DV/Xema/assets/117330523/341f8210-a7a1-4ce7-9eea-eb686f315f43)

在帮助下的关于中，存在相机的基本参数信息。

![image](https://github.com/Open3DV/Xema/assets/117330523/dad6041a-b91a-4e5a-a494-0404d1f78422)

### 20、固件升级

![image](https://github.com/Open3DV/Xema/assets/117330523/86953a2f-2739-4572-a0a2-49f28d58ddfa)

由于产品的更新迭代，导致相机所用固件版本低下，一些新功能无法使用，可通过此方法进行相机的升级，在帮助中，点击固件升级，选择文件，文件通常放在生成的GUI下的update_firmware中，名字叫：camera_server。选择此文件，点击升级即可。注意：在点击升级后，需断电重启相机，方可升级成功。

![image](https://github.com/Open3DV/Xema/assets/117330523/e517cf53-6bee-41a9-b7d5-796d015fd418)

![image](https://github.com/Open3DV/Xema/assets/117330523/545b1bb1-9070-49b5-83dc-8964c2b9cfb7)

![image](https://github.com/Open3DV/Xema/assets/117330523/7f3fdb3e-e7dd-4469-9bba-2f4165ecff44)

### 21、标定参数

![image](https://github.com/Open3DV/Xema/assets/117330523/aa3a21e7-b0fd-4236-bbc7-a0c8550b17be)

在帮助下，存在此款相机的标定参数，包括相机的内参，外参以及畸变系数。

![image](https://github.com/Open3DV/Xema/assets/117330523/ab369fde-a21d-4d4d-a929-301f6edb6fc6)

### 22、加载相机参数、保存相机参数

![image](https://github.com/Open3DV/Xema/assets/117330523/f6830a56-09c6-4f4a-9fa6-4bfcb2c982cd)

在文件下，存在加载相机配置和保存相机配置选项，当我们需要记录下此次拍摄的数据时，我们就可以将配置保存在你想要的文件夹下，当我们下次拍摄时需要用到和上次一样的配置，就可以使用加载相机配置，找到你上次保存的配置进行使用。

![image](https://github.com/Open3DV/Xema/assets/117330523/ad2906bb-cf54-4dd2-a93c-19f3bb94e25b)

### 23、语言

![image](https://github.com/Open3DV/Xema/assets/117330523/09edab48-2291-4449-a4cd-c49997747fa6)

![image](https://github.com/Open3DV/Xema/assets/117330523/307a5dc1-f78d-4976-abb3-631dae256b35)


用户可选择界面进行中英文切换。

![image](https://github.com/Open3DV/Xema/assets/117330523/295604d5-e38a-44df-9526-100581ae7b32)

注意：自行编译的上位机GUI，需要将图中路径的两个翻译文件放入\xema\x64\Release路径下，这样打开GUI才能正常切换语言。

### 24、图标

![image](https://github.com/Open3DV/Xema/assets/117330523/fd41f07a-d693-4b23-abc6-bf3cb301d585)


## 六、典型实例介绍：

本节以普通物体、黑色物体、金属镜面反光工件的顺序着手，由浅入深的讲解如何拍出一副清晰完整的点云图片。但参数不是绝对的，可视工作环境进行微调。

注：本节的点云图片都是在CloudCompare中查看的。

### 1、普通物体

在拍摄普通物体时，在不过曝的情况下，我们要尽量增加投影亮度和曝光时间，此时的拍摄效果将会达到最佳。

首先设置投影亮度最高1023，曝光时间最小20000，置信度为10保留深度信息，这时在亮度图中没有发现过曝现象。但是高度图标注的部分黑色区域没有显示（拍摄的猫咪耳朵位置）。

![image](https://github.com/Open3DV/Xema/assets/117330523/fcaad23e-7378-4807-a981-69adb2f52cfd)

这时可增加重复数，增加有效信息，例如设置为6，如果亮度图此时稍暗，可适当增加曝光时间，如这里从20000增加到22000，再增加将会过曝，应注意！

![image](https://github.com/Open3DV/Xema/assets/117330523/754359af-b0ab-45d2-87d6-2bd4babb32fc)

最终效果如图：

![image](https://user-images.githubusercontent.com/117330523/221113262-6894956e-22da-4493-817e-1105e419c2d1.png)

### 2、黑色物体

拍摄黑色物体，如一块纯黑色的海绵。

首先将投影亮度设置最大1023，曝光时间设置为35000，如果画面不够亮，也可在不过曝的情况下，增加曝光时间。如图所示

![image](https://github.com/Open3DV/Xema/assets/117330523/7b811cb7-1f02-4a3b-8bc9-76d186635a90)

![image](https://github.com/Open3DV/Xema/assets/117330523/4d14f7c8-3732-4c67-b93d-823d14b0019e)

但发现在高度图中海绵有很多的随机噪声，这时我们提高重复数为5，目的是提高信噪比，这样随机噪声将会被抑制，增加了有效信息。如图所示：

![image](https://github.com/Open3DV/Xema/assets/117330523/423cdb19-a934-43c3-b2f9-b26b65c6f7bc)

最后点云效果：

![image](https://user-images.githubusercontent.com/117330523/221113425-1b1576fc-018f-4e4e-aa5f-411ac832c8a3.png)

![image](https://user-images.githubusercontent.com/117330523/221113441-a477aa3d-5ad0-4b90-9c99-311034e079d8.png)

推荐参数（室内照度条件下，仅供参考，可微调）：采用重复曝光

投影亮度：1023，曝光时间：35000，重复曝光数：5，置信度：0，噪点过滤：0。


### 3、金属镜面反光工件（高动态）

![image](https://user-images.githubusercontent.com/117330523/221113466-a69c243c-7622-4004-bf29-b5db24467e44.png)

检测金属、铝箔表面、反光膜片、光滑表面的物品时,镜面反射会造成局部反射光过强,从而失去物体原有信息。

在实际操作环境中，根据物体的层次可选择曝光数，例如上图，有工件、黑色版、带孔平台，这时我们可选择曝光次数为3。

第一步：首先将投影亮度设置为最大1023，将曝光时间设置为30000，目的是能够得到最暗处的深度信息，（置信度为5，噪点过滤为50），这可作为一组高动态下的曝光数据，不打开高动态情况下在高度图中，如图所示，我们可以看到最外层黑色版的深度信息。

![image](https://github.com/Open3DV/Xema/assets/117330523/945a84d4-7c9e-4412-bafa-b4a015888fe6)

第二步：我们要得到最亮处的深度信息，将第一步中工件缺失部分（最亮）的深度信息显示出来。如降低投影亮度为1023，曝光时间为1700，（置信度为5，噪点过滤为50），这可作为一组高动态下的曝光数据，不打开高动态情况下在高度图中，如图所示，可见之前工件缺失（最亮部分）的信息成功显现。

![image](https://github.com/Open3DV/Xema/assets/117330523/415d77fa-c0b3-47ef-8559-995909c24f2e)

第三步：投影亮度设置个第一步和第二步的中间值为800，曝光时间为25000，（置信度为5，噪点过滤为50）可作为一组高动态下的曝光数据，不打开高动态情况下在高度图中，如图所示。

![image](https://github.com/Open3DV/Xema/assets/117330523/abea4f53-9160-459a-857d-5c7e97d8c0b5)

第四步:开启高动态，曝光数设置为3，第一组数据：1700，1023；第二组数据：30000,1023；第三组数据：25000，800。置信度5，噪点过滤50


![image](https://github.com/Open3DV/Xema/assets/117330523/de30ec8e-9891-4c4e-89b6-ec7f5241c059)

如图所示可得到清晰完整的一幅点云图片，无缺失。

![image](https://user-images.githubusercontent.com/117330523/221113668-369ea6f1-8d22-41d7-88b8-11ba2d8834cf.png)

推荐参数（室内照度条件下，仅供参考，可微调）：采用高动态

高动态曝光数：3，噪点过滤：50，置信度：5

采用三组：

1、曝光时间：1700 投影亮度：1023

2、曝光时间：30000 投影亮度：1023

3、曝光时间：25000 投影亮度：800
