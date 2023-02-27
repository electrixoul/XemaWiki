# XEMA系列相机接口文档

## 版本记录

时间 | 版本 | 作者 | 描述
-- | -- | -- | --
2022.02.21 | V1.0.1 | 张观锦 | 完成9个基本函数
2022.03.18 | V1.0.2 | 张观锦 | 完成17个基本函数
2022.05.13 | V1.0.3 | 张观锦 | 完成19个基本函数
2022.06.16 | V1.0.4 | 张观锦 | 完成27个基本函数
2022.08.05 | V1.0.5 | 张观锦 | 完成29个基本函数
2022.09.09 | V1.0.6 | 张观锦 | 完成33个基本函数
2022.11.21 | V1.0.7 | 张观锦 | 完成35个基本函数（修改两个函数）
2023.01.29 | V1.1.0 | 张观锦 | 完成37个基本函数

接口描述

1-33接口在头文件open_cam3d_sdk.h中，34-35接口在头文件enumerate.h中。错误码定义在camera_status.h中。

## 1.Connect

int DfConnect(const char* camera_id);

//函数名： DfConnect

//功能： 连接相机

//输入参数： camera_id（相机ip地址）

//输出参数： 无

//返回值： 类型（int）:返回0表示连接成功;返回-1表示连接失败.

## 2.Disconnect

int DfDisconnect(const char* camera_id);

//函数名： DfDisconnect

//功能： 断开相机连接

//输入参数： camera_id（相机ip地址）

//输出参数： 无

//返回值： 类型（int）:返回0表示断开成功;返回-1表示断开失败.

## 3.Get camera resolution

int DfGetCameraResolution(int* width, int* height);

//函数名： DfGetCameraResolution

//功能： 获取相机分辨率

//输入参数： 无

//输出参数： width(图像宽)、height(图像高)

//返回值： 类型（int）:返回0表示获取参数成功;返回-1表示获取参数失败。

## 4.Capture camera data

int DfCaptureData(int exposure_num, char* &timestamp);

//函数名： DfCaptureData

//功能： 采集点云数据并阻塞至返回结果

//输入参数： exposure_num（曝光次数）：1（为单曝光）、大于1为多曝光（hdr、重复曝光）。

//输出参数： timestamp(时间戳)

//返回值： 类型（int）:返回0表示获取采集点云成功;返回-1表示采集点云失败。
 
## 5.Get Depth Data

int DfGetDepthData(unsigned short* depth);
	//函数名： DfGetDepthData

	//功能： 获取深度图数据

	//输入参数：无

	//输出参数： depth(深度图)

	//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败

参数是相应图像的数据指针，调用方需要根据DfGetCameraResolution返回的结果，提前提前申请好内存空间。数据在内存中将以H（行）/W（列）/C（通道）的顺序排列。

## 6.Get HeightMap Data

//函数名： DfGetHeightMapData

//功能： 获取高度映射图数据

//输入参数：无

//输出参数： height_map(高度映射图)

//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

参数是相应图像的数据指针，调用方需要根据DfGetCameraResolution返回的结果，提前申请好内存空间。数据在内存中将以H（行）/W（列）/C（通道）的顺序排列。

## 7.Get Brightness Data

int DfGetBrightnessData(unsigned short* depth);

	//函数名： DfGetBrightnessData

	//功能： 获取亮度图数据

	//输入参数：无

	//输出参数： brightness(亮度图)

	//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败

参数是相应图像的数据指针，调用方需要根据DfGetCameraResolution返回的结果，提前提前申请好内存空间。数据在内存中将以H（行）/W（列）/C（通道）的顺序排列。

## 8.Get Standard Plane Param

int DfGetStandardPlaneParam(float* R,float* T);

//函数名： DfGetStandardPlaneParam

//功能： 获取基准平面参数

//输入参数：无

//输出参数： R(旋转矩阵：3*3)、T(平移矩阵：3*1)

//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

## 9.Get Height Map Data Base Param

int DfGetHeightMapDataBaseParam(float* R, float* T, float* height_map);

//函数名： DfGetHeightMapDataBaseParam

//功能： 获取校正到基准平面的高度映射图

//输入参数：R(旋转矩阵)、T(平移矩阵)

//输出参数： height_map(高度映射图)

//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败。

## 10.Get Pointcloud Data

int DfGetPointcloudData(float* point_cloud);	

//函数名： DfGetPointcloudData

	//功能： 获取点云数据（深度图转点云）

	//输入参数：无

	//输出参数： point_cloud(点云)

	//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败

参数是相应图像的数据指针，调用方需要根据DfGetCameraResolution返回的结果，提前提前申请好内存空间。数据在内存中将以H（行）/W（列）/C（通道）的顺序排列。

## 11.Get calibration parameters

int DfGetCalibrationParam(struct CalibrationParam* calibration_param);

//函数名： DfGetCalibrationParam

//功能： 获取相机标定参数

//输入参数： 无

//输出参数： calibration_param（相机标定参数结构体）

//返回值： 类型（int）:返回0表示获取标定参数成功;返回-1表示获取标定参数失败.

## 12.Set Led Current parameters

int DfSetParamLedCurrent(int led);

//函数名： DfSetParamLedCurrent

//功能： 设置LED电流

//输入参数： led（电流值）

//输出参数： 无

//返回值： 类型（int）:返回0表示获取标定参数成功;返回-1表示获取标定参数失败.

## 13.Get Led Current parameters

int DfGetParamLedCurrent(int led);

	//函数名： DfGetParamLedCurrent

	//功能： 设置LED电流

	//输入参数： 无

	//输出参数： led（电流值）

	//返回值： 类型（int）:返回0表示获取标定参数成功;返回-1表示获取标定参数失败.

## 14.Set Hdr parameters

int DfSetParamMixedHdr(int num, int exposure_param[6], int led_param[6]);

	//函数名： DfSetParamMixedHdr

	//功能： 设置混合多曝光参数（最大曝光次数为6次）

	//输入参数： num（曝光次数）、exposure_param[6]（6个曝光参数、前num个有效）、led_param[6]（6个led亮度参数、前num个有效）

	//输出参数： 无

	//返回值： 类型（int）:返回0表示获取标定参数成功;返回-1表示获取标定参数失败.


## 15.Get Hdr parameters

int DfGetParamMixedHdr(int& num, int exposure_param[6], int led_param[6]);

	//函数名： DfGetParamMixedHdr

	//功能： 获取混合多曝光参数（最大曝光次数为6次）

	//输入参数： 无

	//输出参数： num（曝光次数）、exposure_param[6]（6个曝光参数、前num个有效）、led_param[6]（6个led亮度参数、前num个有效）

	//返回值： 类型（int）:返回0表示获取标定参数成功;返回-1表示获取标定参数失败.

## 16.Set Standard Plane parameters

int DfSetParamStandardPlaneExternal(float* R, float* T);

	//函数名： DfSetParamStandardPlaneExternal

	//功能： 设置基准平面的外参

	//输入参数：R(旋转矩阵：3*3)、T(平移矩阵：3*1)

	//输出参数： 无

	//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

## 17.Get Standard Plane parameters

int DfGetParamStandardPlaneExternal(float* R, float* T);

	//函数名： DfGetParamStandardPlaneExternal

	//功能： 获取基准平面的外参

	//输入参数：无

	//输出参数： R(旋转矩阵：3*3)、T(平移矩阵：3*1)

	//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

## 18.Set Camera Exposure Parameters

int DfSetParamCameraExposure(float exposure);

	//函数名： DfSetParamCameraExposure

	//功能： 设置相机曝光时间

	//输入参数：exposure(相机曝光时间)

	//输出参数： 无

	//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

## 19.Get Camera Exposure Parameters

int DfGetParamCameraExposure(float& exposure);

	//函数名： DfGetParamCameraExposure

	//功能： 获取相机曝光时间

	//输入参数： 无

	//输出参数：exposure(相机曝光时间)

	//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

## 20.Get Mixed Hdr Parameters

int DfGetParamMixedHdr(int& num, int exposure_param[6], int led_param[6]);

//函数名： DfGetParamMixedHdr

//功能： 获取混合多曝光参数（最大曝光次数为6次）

//输入参数： 无

//输出参数： num（曝光次数）、exposure_param[6]（6个曝光参数、前num个有效）、led_param[6]（6个led亮度参数、前num个有效）

//返回值： 类型（int）:返回0表示获取标定参数成功;返回-1表示获取标定参数失败. 

## 21.Set Camera Confidence Parameters

int DfSetParamCameraConfidence(float confidence);

//函数名： DfSetParamCameraConfidence

//功能： 设置相机曝光时间

//输入参数：confidence(相机置信度)

//输出参数： 无

//返回值：类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

## 22.Set Mixed Hdr Parameters

int DfSetParamMixedHdr(int num, int exposure_param[6], int led_param[6]);

//函数名： DfSetParamMixedHdr

//功能： 设置混合多曝光参数（最大曝光次数为6次）

//输入参数： num（曝光次数）、exposure_param[6]（6个曝光参数、前num个有效）、led_param[6]（6个led亮度参数、前num个有效）

//输出参数： 无

//返回值： 类型（int）:返回0表示获取标定参数成功;返回-1表示获取标定参数失败.

## 23.Get Camera Confidence Parameters

int DfGetParamCameraConfidence(float& confidence);

//函数名： DfGetParamCameraConfidence

//功能： 获取相机曝光时间

//输入参数： 无

//输出参数：confidence(相机置信度)

//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.


## 24.Set Camera Gain Parameters

int DfSetParamCameraGain(float gain); 

//函数名： DfSetParamCameraGain

//功能： 设置相机增益

//输入参数：gain(相机增益)

//输出参数： 无

//返回值：类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

## 25.Get Camera Gain Parameters

int DfGetParamCameraGain(float& gain);

//函数名： DfGetParamCameraGain

//功能： 获取相机增益

//输入参数： 无

//输出参数：gain(相机增益)

//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

## 26.Set Pointcloud Smoothing Parameters

int DfSetParamSmoothing(int smoothing);

//函数名： DfSetParamSmoothing

//功能： 设置点云平滑参数

//输入参数：smoothing(0:关、1-5:平滑程度由低到高)

//输出参数： 无

//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.


## 27.Get Pointcloud Smoothing Parameters

int DfGetParamSmoothing(int& smoothing);

//函数名： DfGetParamSmoothing

//功能： 设置点云平滑参数

//输入参数：无

//输出参数：smoothing(0:关、1-5:平滑程度由低到高)

//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.


## 28.Set Radius Filter Parameters

int DfSetParamRadiusFilter(int use,float radius,int num);
//函数名： DfSetParamRadiusFilter

//功能： 设置点云半径滤波参数

//输入参数：use(开关：1开、0关)、radius(半径）、num（有效点）

//输出参数： 无

//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

## 29.Get Radius Filter Parameters

int DfGetParamRadiusFilter(int& use, float& radius, int& num);

//函数名： DfGetParamRadiusFilter

//功能： 获取点云半径滤波参数

//输入参数：无

//输出参数：use(开关：1开、0关)、radius(半径）、num（有效点）

//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

## 30.Set Outlier Filter Parameters

int DfSetParamOutlierFilter(float threshold);

//函数名： DfSetParamOutlierFilter

//功能： 设置外点过滤阈值

//输入参数：threshold(阈值0-100)

//输出参数： 无

//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

## 31.Get Outlier Filter Parameters

int DfGetParamOutlierFilter(float& threshold);	

//函数名： DfGetParamOutlierFilter

//功能： 获取外点过滤阈值

//输入参数： 无

//输出参数：threshold(阈值0-100)

//返回值： 类型（int）:返回0表示获取数据成功;返回-1表示采集数据失败.

## 32.Set Multiple Exposure Model Parameters

int DfSetParamMultipleExposureModel(int model);

//函数名： DfSetParamMultipleExposureModel

//功能： 设置多曝光模式

//输入参数： model(1：HDR(默认值)、2：重复曝光)

//输出参数：无

//返回值： 类型（int）:返回0表示设置参数成功;否则失败。

## 33.Set Repetition Exposure Num Parameters

int DfSetParamRepetitionExposureNum(int num);

//函数名： DfSetParamRepetitionExposureNum

//功能： 设置重复曝光数

//输入参数： num(2-10)

//输出参数：无

//返回值： 类型（int）:返回0表示设置参数成功;否则失败。 

## 34.Update Device List

int DfUpdateDeviceList(int& device_num);
	
//函数名： DfUpdateDeviceList

//功能： 获取可连接设备数

//输入参数： device_num(设备数)

//输出参数： 无

//返回值： 类型（int）:返回0表示连接成功;返回-1表示连接失败.

## 35.Get All Device Base Info

int DfGetAllDeviceBaseInfo(DeviceBaseInfo* pDeviceInfo, int* pBufferSize);

//函数名： DfGetAllDeviceBaseInfo

//功能： 获取设备基本信息

//输入参数： pDeviceInfo(设备信息)、pBufferSize（设备结构体内存尺寸）

//输出参数： 无

//返回值： 类型（int）:返回0表示连接成功;返回-1表示连接失败.

## 36.Set Depth Filter Parameters

int DfSetParamDepthFilter(int use, float depth_filter_threshold);

//函数名： DfSetParamRadiusFilter

//功能： 设置深度图滤波参数

//输入参数：use(开关：1开、0关)、depth_filterthreshold(过滤的噪声阈值)

//输出参数： 无

//返回值： 类型（int）:返回0表示设置参数成功;否则失败。

## 37.Get Depth Filter Parameters

int DfGetParamDepthFilter(int& use, float& depth_filter_threshold);

//函数名： DfSetParamRadiusFilter

//功能： 设置深度图滤波参数

//输入参数：无

//输出参数： use(开关：1开、0关)、depth_filterthreshold(距离过滤的噪声阈值)

//返回值： 类型（int）:返回0表示获取参数成功;否则失败。

 例程

详细请看example.cpp

属性说明

//相机标定参数结构体

struct CalibrationParam

{

	//相机内参

	double intrinsic[3*3];

	//相机外参

	double extrinsic[4*4];

	//相机畸变

//<k1,k2,p1,p2,k3,k4,k5,k6,s1,s2,s3,s4>暂时只使用5个畸变参数

	double distortion[1*12];

};

//设备基本信息结构体

struct DeviceBaseInfo

{

	//相机内参

	char mac[64];

	//相机外参

	char ip[64];  

};


## 错误码

错误码 | 码值 | 描述
-- | -- | --
DF_SUCCESS | 0 | 成功
DF_FAILED | -1 | 失败
DF_UNKNOWN | -2 | 未知命令
DF_BUSY | -3 | 相机占用
DF_NOT_CONNECT | -4 | 相机未连接
DF_ERROR_NETWORK | -5 | 网络出错
DF_ERROR_2D_CAMERA | -6 | 2d相机故障
DF_ERROR_INVALID_PARAM | -7 | 无效参数
DF_ERROR_LIGHTCRAFTER_SET_MODEL | -8 | 光机投影模式设置出错
DF_ERROR_LIGHTCRAFTER_SET_TRIGGEROUT | -9 | 光机触发设置出错
DF_ERROR_LIGHTCRAFTER_SET_CURRENT | -10 | 光机设置亮度出错
DF_ERROR_LIGHTCRAFTER_SET_PATTERN_ORDER | -11 | 光机条纹设置出错
DF_ERROR_CAMERA_STREAM | -12 | 相机操作流出错
DF_ERROR_CAMERA_GRAP | -13 | 相机采图出错
DF_FRAME_CAPTURING | -14 | 相机正在采集帧数据