# Operating Instructions of XEMA

## V1.0.7

![image](https://user-images.githubusercontent.com/117330523/221140452-a1a5e148-6b1c-4c02-b2d3-cc6141b29562.png)

## 1.Product Presentation

XEMA series cameras are structured light 3D cameras based on DLP projection, which are suitable for use scenarios such as 3D scanning, industrial 3D defect detection, industrial disorderly grabbing with industrial robots, and loading and unloading. The core components include TI DLP3010 projection chip, Sony IMX174 imaging chip and Nvidia Jetson Nano computing module. The data transmission of XEMA uses the GigE interface and XEMA supports multiple exposure modes.

## 2.Product Display

![image](https://user-images.githubusercontent.com/117330523/221140542-ffc75653-ca59-49fd-85b3-01f5f5343f45.png)

![image](https://user-images.githubusercontent.com/117330523/221140572-cb4d01c5-e941-4b46-870c-90ddd143c2c2.png)

## 3.Performance description

Parameter | Value
-- | --
Calibration accuracy | 0.05/mm
Point cloud resolution | 1920x1200
Image resolution | 1920x1200
Frame rate | 1fps
Baseline length | 150mm
Working distance | 400 ~ 2000mm
Data interface | Ethernet
Horizontal field of view | 40°
Vertical field of view | 23°
Product size | 207 × 128 × 50.5 mm
Product weight | 1000g
CPU | Quad-core Arm A57 processor @ 1.43 GHz
GPU | 128-core Maxwell GPU
Memory | 4GB 64-bit LPDDR4

## 4. Product Installation Instructions

### 4.1 Product Accessories

![image](https://user-images.githubusercontent.com/117330523/221141023-5b02b37e-f8e5-400f-b036-f2ee3e4bbdc7.png)

### 4.2 Hardware connection

There are two ways for computers to access the camera through the network, one is through the router connection to interact, and the other is through the network cable direct connection to communicate. 

![image](https://user-images.githubusercontent.com/117330523/221141063-aa724866-da4f-4f88-8a64-f0096515c541.png)

![image](https://user-images.githubusercontent.com/117330523/221141114-b55f4755-45f8-4666-97d5-f1432044a843.png)


First, we should confirm that the power cord and the network cable are firmly connected before the camera is powered on. Then after the Power is turned on, the "Power" indicator is always on, and the camera starts up for about 30 seconds, at this time, the green indicator of the network port of the camera is always on, and the orange indicator is flashing, indicating that the network bandwidth is gigabit. The camera's "Act" indicator lights up during photography and data transmission, and is usually off.

### 4.3 Software Interface

4.3.1 ConfiguringIP interface introduction

First, Open configuring_network_gui.exe and then click Search Camera, the display interface is as shown in he figure below.

![image](https://user-images.githubusercontent.com/117330523/221141657-1ff249e9-12f0-46df-ad2a-4e6b593d527a.png)

 The searched cameras will be displayed in a list. The left column is the MAC address of the camera, and the right column is the camera IP. When the camera is directly connected to the computer, the negotiated IP address searched after booting is similar to the figure below.the figure below. 

![image](https://user-images.githubusercontent.com/117330523/221141701-386fa9d9-ee93-4567-baab-8ec2377fb5c5.png)


4.3.2 OpenCam3D interface introduction

![image](https://user-images.githubusercontent.com/117330523/221141854-164e9bd6-381a-4da5-8e8d-adbfba897b0e.png)

After opening the interface, enter the IP address searched in 4.3.1, and fill it in the red address bar, and click the connection button above the address bar to connect the camera for subsequent operations. If the connection is successful, the information bar at the bottom left of the interface will display Prompt that the connection is successful.

![image](https://user-images.githubusercontent.com/117330523/221141918-ff281560-80cd-4fdd-9a38-47b0f81ebca3.png)

Click the camera icon in the red box, the camera will shoot and display the captured image on the right, and you can select the brightness map/depth map/height map on the upper right of the display box to view them separately. In order to get the best and effective image data, the projection brightness and exposure time can be modified in the left setting bar. Click the save button on the right side of the photo, and you can save the captured brightness map, point cloud map, etc. to the computer, or you can check the automatic save to automatically save the picture after shooting. In addition to the above settings, the interface also provides parameters such as gain, confidence, smoothing, and number of repeated shots, etc. for configuration.

## 5.Product introduction for use

### 5.1 High dynamic range

High dynamic range imaging is a group (HDRI/HDR) of techniques used to achieve a greater dynamic range of exposure (ie, a greater difference between light and dark) than ordinary digital imaging techniques.

Effect: HDRI will make the picture layer more distinct, and the difference between light and dark is obvious.

Method of use: Set the number of exposures to take multiple exposures.

Number of exposures: It is the number of exposures, used with HDR method. In HDR mode, we can choose the number of exposures you need (range: 1-6). When HDR mode is required, please observe the picture to choose the number of exposures. In HDR mode, exposure time and projected brightness are one group. The interface is shown in the figure below.  

![image](https://user-images.githubusercontent.com/117330523/221142022-b0f1c064-d912-48d0-a7a1-67fbef9a8951.png)

Notice: The default number of high dynamic groups is 2, and it is recommended to use fewer groups if the quality of the point cloud is satisfied. In Typical Example 3, the specific usage methods of high dynamics will be introduced.

Number of groups (data can be modified):

![image](https://user-images.githubusercontent.com/117330523/221142100-a37f8813-7d91-404e-b2b5-5ef5f5dc1160.png)

![image](https://user-images.githubusercontent.com/117330523/221142139-337cce04-d194-4f2f-b62b-a89c9b1b4c80.png)

![image](https://user-images.githubusercontent.com/117330523/221142169-16ca30d9-3eec-40bf-9ef1-6696a21159fd.png)

### 5.2 Camera exposure time

![image](https://user-images.githubusercontent.com/117330523/221142232-07850ad1-5315-49e8-b248-09b7a0f18be6.png)

Range：1700-100000

Camera exposure time: Exposure time is the time for the shutter to open when the reflected light of the scene reaches the imaging photosensitive material through the lens. The simple explanation is the time when the light enters the camera when the shutter of the camera is open.

The longer the exposure time, the more light gets in. If the exposure time is too long, overexposure will occur. For overexposure viewing: Turn on the overexposure display switch, and the red part in the brightness graph is the overexposure area.

![image](https://user-images.githubusercontent.com/117330523/221142321-5fcf071f-364a-4046-9e41-067f6b944d82.png)

![image](https://user-images.githubusercontent.com/117330523/221142358-b34b1c13-a844-46fa-8fc8-a304bf9eadc4.png)

### 5.3 Projection brightness

![image](https://user-images.githubusercontent.com/117330523/221142392-f88b39d1-bcf6-4557-9bba-0f194a40dd79.png)

Range：0-1023

Notice: Priority use the brightness 1023

Projection brightness: It refers to the intensity of projected light. The greater the light intensity, the brighter and clearer the image. Within a certain range, the human eye will feel that the picture is clearer because of the high brightness. If it exceeds this limit, it will be too strong. Brightness can make it impossible to see the image.

![image](https://user-images.githubusercontent.com/117330523/221142491-5f2a52cf-b150-4e3f-b30e-3c827cf7f1d5.png)

![image](https://user-images.githubusercontent.com/117330523/221142523-25599196-1301-48d7-b028-75347b2f1dea.png)

### 5.4 Overexposure display

When we are shooting, it is inevitable that there will be overexposure. In the brightness map, we can check the overexposure button to observe the overexposure area, so that you can change related parameters, such as exposure time, brightness, HDR mode, etc. operation to correct.

![image](https://user-images.githubusercontent.com/117330523/221142571-771d84f7-24fa-42e5-89b4-24f9f2267a33.png)

![image](https://user-images.githubusercontent.com/117330523/221142607-20bbbb0c-ddbe-4374-bffb-b0d9344015f7.png)

### 5.5 Confidence

![image](https://user-images.githubusercontent.com/117330523/221142722-a3c44a96-1b90-4e95-ab47-6382762d9447.png)

Range: 0-100

When the confidence level is lowered, the depth information (depth map) of the black part will be retained.

![image](https://user-images.githubusercontent.com/117330523/221142795-7f25cf6c-1390-4a2b-b535-f17ca0345a23.png)

On the contrary, the black noise will be removed after the confidence level is increased.

![image](https://user-images.githubusercontent.com/117330523/221142852-6e1250ba-0981-4be6-bb12-8e033398cdf3.png)

### 5.6 Noise filtering

![image](https://user-images.githubusercontent.com/117330523/221142898-25a67160-e5fc-4ab3-9a5e-349a4da9ce86.png)

Range: 0-100

In machine vision application scenarios, such as detecting metal, aluminum foil surface, reflective film, and items with smooth surfaces, specular reflection will cause local reflected light to be too strong, thereby losing the original information of the object and interfering with machine vision detection. Noise filtering can eliminate part of the generated noise and preserve the original information of the object.

![image](https://user-images.githubusercontent.com/117330523/221142957-e455ed41-1927-40c9-a3af-4e3d6020794f.png)

![image](https://user-images.githubusercontent.com/117330523/221142985-5262c66e-a2e9-4ae0-b061-998fa6299d1f.png)

### 5.7 Get brightness map

The function of generating a brightness map is at the bottom of the interface. It has three modes: default, custom lighting, and custom non-lighting. Generally, the default mode is used. The custom light-emitting mode can set the exposure time by itself; The custom non-light-emitting mode uses the brightness of the light in the environment.

![image](https://user-images.githubusercontent.com/117330523/221143051-ab2a2701-c8da-42e9-9224-44cd0df2373c.png)
 
### 5.8 Datum plane parameters

Height mapping datum plane: The datum plane is a plane at the datum zero position, and the photographed object (such as the calibration plate) is taken as the datum zero position. If the X-axis and Y-axis of the calibration plate are known, the Z-axis direction can be judged according to the right-hand rule. The calibration plate is the reference plane, the front of the calibration plate is the negative direction of Z-axis (closer to the camera), and the reverse side of the calibration plate is the positive direction of Z-axis (away from the camera). 

![image](https://user-images.githubusercontent.com/117330523/221143149-800b750e-f3e3-4ac5-a3ad-9cb14203056a.png)

The datum parameters are measured from data and cannot be modified.

For example:

![image](https://user-images.githubusercontent.com/117330523/221143263-d57ff0c2-a170-4226-a865-739cc799b859.png)

![image](https://user-images.githubusercontent.com/117330523/221143320-9f6e5bb4-bc5a-4078-bce7-40a3de5af716.png)

![image](https://user-images.githubusercontent.com/117330523/221143351-7c9c6359-9d34-4a88-9ec0-07f318c318d9.png)

### 5.9 Maximum height and minimum height

![image](https://user-images.githubusercontent.com/117330523/221143471-28ff4aa6-d83e-4e48-9b76-93ced54e692a.png)

Maximum height (maximum value): 9999.99 

Minimum height (minimum value): -9999 

If we want to use the height map and only want to view the object, we can adjust the maximum height and the minimum height. We have known that the calibration plate (the plate can be replaced by other objects) is the reference plane, and it is negative when it is close to the camera, and it is positive when it is far away from the camera. 


![image](https://user-images.githubusercontent.com/117330523/221143566-e0050a55-5982-4bd4-84fb-83aaea2e3c25.png)


For example, if we only want to display the selected metal workpiece, we only need to set the maximum height below 0mm, such as this setting -1mm (close to the reference plane), and the minimum height must be equal to or exceed the length of the workpiece, such as this setting -600mm. The effect is that all scenes other than the workpiece are not displayed, and only the height map of the workpiece is kept. As shown below:

![image](https://user-images.githubusercontent.com/117330523/221143608-c8e29368-3881-443d-87a8-46a3d0c480dd.png)

### 5.10 Gain

![image](https://user-images.githubusercontent.com/117330523/221143653-4aafd39d-ce0c-4beb-85d3-4cdd5dcf79a4.png)

Range: 0-10.

Gain: It is used to adjust the brightness and darkness of the picture, and it is not recommended to set it.

### 5.11 Radius filtering

![image](https://user-images.githubusercontent.com/117330523/221143735-2cc8bf48-0a98-40ad-8114-7bb477e0a83e.png)

![image](https://user-images.githubusercontent.com/117330523/221143777-87af6f9b-26c8-4068-a7f9-6604e59ce558.png)

Radius range: 0-99.99

Effective point range: 0-99

For each point in the point cloud, a sphere with the radius of r is determined, and the number of effective points is selected. If the number of internal points is less than the effective point, it is considered to be a noise point and should be eliminated.

### 5.12 Depth filtering

![image](https://user-images.githubusercontent.com/117330523/221143821-d8cdeb16-cabc-4030-8479-a3a7f71bb208.png)

It is a filtering method based on the depth map, which is enabled by checking. The recommended threshold is 33 at a distance of 1000mm.

### 5.13 Calibration plate model

Model selection: 4mm/12mm/20mm/40mm/80mm

![image](https://user-images.githubusercontent.com/117330523/221143895-98574be5-7470-48e4-ac90-3c99267a705c.png)

![image](https://user-images.githubusercontent.com/117330523/221143929-cfff5ab0-b7d5-4552-90b1-57759f19b8d0.png)

### 5.14 Camera IP address: ***.***.***.***

![image](https://user-images.githubusercontent.com/117330523/221143955-f98729c8-11d0-4538-a95c-5b850da54c2c.png)

### 5.15 Number of Repeat exposures

![image](https://user-images.githubusercontent.com/117330523/221144127-9b285eac-7df1-4199-bb98-557913ea6c36.png)

Range: 0-10

It is the number of times the camera needs to repeat shooting. It can increase the signal-to-noise ratio (the ratio of signal to noise). The effect is better if the signal-to-noise ratio is higher, so that random noise will be suppressed and effective information will be increased.

### 5.16 Icon

![image](https://user-images.githubusercontent.com/117330523/221144294-3269ac53-8ca0-4a06-8af7-8f7e7306e102.png)

![image](https://user-images.githubusercontent.com/117330523/221144388-50c30f85-8e4e-47bf-98f7-762dde1c5b82.png)

## 6. Typical examples

This section starts with the order of ordinary objects, black objects, and metal mirror reflective workpieces, and explains how to take a clear and complete point cloud picture from the shallower to the deeper. But the parameters are not absolute, and they can be fine-tuned depending on the working environment.

Notice: The point cloud images in this section are all viewed in CloudCompare.

### 6.1 Ordinary objects

When shooting ordinary objects under the condition of not overexposure, we should try to increase the projection brightness and exposure time, and the shooting effect will be the best at this time.

First, we set the highest projection brightness to 1023, and the minimum exposure time to 20000, and the confidence level to 10 to retain the depth information. At this time, no overexposure phenomenon is found in the brightness map. But part of the black area marked on the height map is not displayed (the position of the cat's ears in the image).

![image](https://user-images.githubusercontent.com/117330523/221144587-5a9896ac-5cfa-411e-9b5c-4328a5af84c8.png)

At this time, we can increase the number of repetitions and increase the effective information. For example, set it to 6. If the brightness map is slightly dark at this time, we can increase the exposure time appropriately. For example, we can increase the exposure time from 20000 to 22000. But it will be overexposed If we keep increasing the exposure time. Please pay attention it!

![image](https://user-images.githubusercontent.com/117330523/221144825-e9034f9e-7122-4a5c-a524-c1ed0786a0a6.png)

The final effect is shown in the figure below:


![image](https://user-images.githubusercontent.com/117330523/221144876-145504ab-0c0e-4136-b5dc-447fb80ee973.png)

### 6.2 Black objects

We shoot a black sponge. First, we set the maximum projection brightness to 1023, and set the exposure time to 35000. If the picture is not bright enough, you can also increase the exposure time without overexposure. As shown below:

![image](https://user-images.githubusercontent.com/117330523/221144915-3cab3d08-c137-490f-abfa-3accb9875387.png)

![image](https://user-images.githubusercontent.com/117330523/221144970-f13cff14-dbd1-458b-8272-d134d13ec836.png)

We found that there is a lot of random noise in the sponge in the height map. At this time, we increased the number of repetitions to 5 to improve the signal-to-noise ratio, so that the random noise will be suppressed and the effective information will be increased. As shown below:

![image](https://user-images.githubusercontent.com/117330523/221145019-44612b6e-2a7e-45b0-844b-cba27768ca10.png)

The final point cloud effect:

![image](https://user-images.githubusercontent.com/117330523/221145106-c21982b7-f06e-49ab-b9ab-264277ec3236.png)

![image](https://user-images.githubusercontent.com/117330523/221145064-796515b2-1ee8-44ad-89e3-6e117af4202b.png)

### 6.3 Metal specular reflective workpieces (HDR)

![image](https://user-images.githubusercontent.com/117330523/221145158-e587fbea-967a-4eed-b140-5a512655eba0.png)

When detecting metal, aluminum foil surface, reflective film, and smooth surface items, the specular reflection will cause local reflected light to be too strong, and thus losing the original information of the object.

In the actual operating environment, the number of exposures can be selected according to the level of the object. For example, in the above picture, there are workpieces, black plates, and platforms with holes. At this time, we can choose the number of exposures to be 3.

Step 1: First, we set the projection brightness to the maximum 1023, and set the exposure time to 30000 (the confidence level is 5, and the noise filter is 50), which can be able to get the depth information of HDR. In the height map without turning on the HDR, as shown in the figure, we can see the depth information of the outermost black version.

![image](https://user-images.githubusercontent.com/117330523/221145201-1343e763-ac36-45ff-ae96-7576b8362e88.png)

Step 2: We want to get the depth information of the brightest part, and display the depth information of the missing part (brightest) of the workpiece in the first step. For example, the projection brightness is reduced to 1023, the exposure time is 1700 (the confidence level is 5, and the noise filter is 50), which can be used as a set of exposure data under HDR. In the height map without turning on the HDR, as shown in the figure, it can be seen that the missing (brightest part) information of the previous artifact is successfully displayed.

![image](https://user-images.githubusercontent.com/117330523/221145243-19feb3fe-7494-4dea-a132-910d4b42b739.png)

Step 3: Set the projection brightness is the intermediate value (800) of the step 1 and the step 2, and the exposure time is 25000. (The confidence level is 5, and the noise filter is 50). It can be used as a set of exposure data under HDR. In the height map without turning on the HDR, as shown in the figure.

![image](https://user-images.githubusercontent.com/117330523/221145284-309c5eb1-0b6a-446e-b4ff-95081f91669a.png)

Step 4: Turn on HDR, and set the number of exposures to 3.The first set of data: 1700, 1023; The second set of data: 30000, 1023; The third set of data: 25000, 800. (Confidence level 5, noise filtering 50).

![image](https://user-images.githubusercontent.com/117330523/221145339-4dcc7e8f-8540-4514-a008-d6b73eb946dd.png)

As shown in the figure, a clear and complete point cloud picture can be obtained without loss.

![image](https://user-images.githubusercontent.com/117330523/221145398-3178d708-7991-4624-9423-c457d6bf6ec4.png)
