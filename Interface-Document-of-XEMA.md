# Interface Document of XEMA 

## Version Record

Time | Version | Author | Description
-- | -- | -- | --
2022.02.21 | V1.0.1 | Guanjin Zhang | Complete 9 basic functions
2022.03.18 | V1.0.2 | Guanjin Zhang | Complete 17 basic functions
2022.05.13 | V1.0.3 | Guanjin Zhang | Complete 19 basic functions
2022.06.16 | V1.0.4 | Guanjin Zhang | Complete 27 basic functions
2022.08.05 | V1.0.5 | Guanjin Zhang | Complete 29 basic functions
2022.09.09 | V1.0.6 | Guanjin Zhang | Complete 33 basic functions
2022.11.21 | V1.0.7 | Guanjin Zhang | Complete 35 basic functions（Modified 2 functions）
2023.01.29 | V1.1.0 | Guanjin Zhang | Complete 37 basic functions

Interface description 

ConnectInterfaces are in the header file of open_cam3d_sdk.h.

Error Codes are defined in camera_status.h.

1.Connect

    // Name of function:  DfConnect

    // Function:  Connect camera

    // Input parameter:  camera_id (Camera ip address)

    // Output parameter:  None

    // Return value:  Type(int): 0 means the connection failed; 1 means the connection success

    int DfConnect(const char* camera_id);

2.GetCameraResolution
    // Name of function:  DfGetCameraResolution

    // Function:  Get the camera resolution

    // Input parameter:  None

    // Output parameter:   width(image width),  height(image height)

    // Return value:  Type(int): 0 means the parameter acquisition success; -1 means the parameter acquisition failed.

    DF_SDK_API int  DfGetCameraResolution(int* width, int* height);

 3.DfSetCaptureEngine
    //Name of function: DfSetCaptureEngine

    //Function：Set up the collection engine

    //Input parameter: engine

    //Output parameter: 

    //Return value: Type(int): 0 means the parameter acquisition success; -1 means the parameter acquisition failed.

    DF_SDK_API int DfSetCaptureEngine(XemaEngine engine);

4.GetCaptureEngine

    //Name of function: DfGetCaptureEngine

    //Function： Gets the capture engine mode

    //Input parameter:：
 
    //Output parameter：engine

    //Return value: Type(int): 0 means the parameter acquisition success; -1 means the parameter acquisition failed.

    DF_SDK_API int DfGetCaptureEngine(XemaEngine& engine);

5.CaptureData

    // Name of function:  DfCaptureData

    // Function:  Collect point cloud data and block until the result is returned

    // Input parameter:  Exposure_num (Exposure times (repeated exposure when >1) ) 

    // Output parameter:  timestamp (value of timestamp)

    // Return value:  Type(int): 0 means the point cloud acquisition success; -1 means the point cloud acquisition failed.

    DF_SDK_API int DfCaptureData(int exposure_num, char* timestamp);

6.GetDepthData
 
    // Name of function:  DfGetDepthData

    // Funciton:  Get depth map data
 
    // Input parameter:  None

    // Out parameter:  depth (depth map)

    // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

    DF_SDK_API int DfGetDepthData(unsigned short* depth);


The parameter is the data pointer corresponding to the image and the caller needs to apply for memory space in advance according to the return result of function DfGetCameraResolution.

The data will be arranged in the order of H (row)/W (column)/C (channel) in the memory.


7.GetDepthDataFloat

    // Name of function:  DfGetDepthDataFloat

    // Funciton:  Get depth map data

    // Input parameter:  None

    // Out parameter:  depth (depth map)

    // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.
 
    DF_SDK_API int DfGetDepthDataFloat(float* depth);

8.GetUndistortDepthDataFloat

    //Name of function:  DfGetUndistortDepthDataFloat

    //Funciton: Get the depth map after the distortion is removed

    // Input parameter:  None

    // Out parameter:  depth (depth map)

    // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

    DF_SDK_API int DfGetUndistortDepthDataFloat(float* depth);

9.GetBrightnessData

    // Name of function:  DfGetBrightnessData

    // Funciton:  Get brightness data

    // Input parameter:  None

    // Onput parameter:  brightness(data of brightness map)

    // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

    DF_SDK_API int DfGetBrightnessData(unsigned char* brightness);

10.GetUndistortBrightnessData

    //Name of function: DfGetUndistortBrightnessData

    //Funciton: Obtain the brightness map after removing the distortion

    // Input parameter:  None

    // Onput parameter:  brightness(data of brightness map)

    // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

    DF_SDK_API int DfGetUndistortBrightnessData(unsigned char* brightness);
 
	
11.GetHeightMapData

     // Name of function:  DfGetHeightMapData

     // Funciton:  Get height map data

     // Input parameter:  None

     // Onput parameter:  height_map (data of height map)

     // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

     DF_SDK_API int DfGetHeightMapData(float* height_map);

12.GetStandardPlaneParam

    // Name of function:  DfGetStandardPlaneParam

    // Funciton:  Get datum plane parameters

    // Input parameter:  None

    // Output parameter:  R(rotation matrix: 3*3),   T(Translation matrix: 3*1)

    // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

    DF_SDK_API int DfGetStandardPlaneParam(float* R, float* T);

13.GetHeightMapDataBaseParam

    // Name of function:  DfGetHeightMapDataBaseParam

    // Funciton:  Get the height map corrected to the datum plane

    // Input parameter:  R(rotation matrix: 3*3),   T(Translation matrix: 3*1)

    // Output parameter:  height_map (data of height map)

    // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.	DF_SDK_API int 

    DfGetHeightMapDataBaseParam(float* R, float* T, float* height_map);

14.GetPointcloudData

    // Name of function:  DfGetPointcloudData

    // Funciton:  Get the data of point cloud (depth map to point cloud)

    // Input parameter:  None
 
    // Output parameter:  point_cloud (data of point cloud)

    // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

    DF_SDK_API int DfGetPointcloudData(float* point_cloud);

15.Disconnect

    // Name of function:  DfDisconnect

    // Function:  Disconnect camera

    // Input parameter:  camera_id (Camera ip address)

    // Output parameter:  None

    // Return value:  Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfDisconnect(const char* camera_id);

16.GetCalibrationParam

    // Name of function:  DfDisconnect

    // Function:  Disconnect camera

    // Input parameter:  camera_id (Camera ip address)

    // Output parameter:  None

    // Return value:  Type(int): 0 means the disconnection success; -1 means the connection failed.

	DF_SDK_API int DfGetCalibrationParam(struct CalibrationParam* calibration_param);


	/***************************************************************************************************************************************************************/

	//parameter setting


17.SetParamLedCurrent

    // Name of function:  DfSetParamLedCurrent

    // Funciton:  Set the current of LED

    // Input parameter:  led (current)

    // Output parameter:  None

    // Return value:  type (int):  0 means the parameter setting success; -1 means the parameter setting failed.	

    DF_SDK_API int DfSetParamLedCurrent(int led);


18.GetParamLedCurrent

    // Name of function:  DfGetParamLedCurrent

    // Funciton:  Get the current of LED

    // Input parameter:  None

    // Output parameter:  led (current)

    // Return value:  type (int):  0 means the parameter acquisition success; -1 means the parameter acquisition failed.

    DF_SDK_API int DfGetParamLedCurrent(int& led);


19.SetParamHdr

    // Name of function:  DfSetParamHdr

    // Funciton:  Set the parameters for repeated exposures (maximum exposure number of times is 6)

    // Input parameter:  num(exposure times),  exposure_param[6] (6 exposure parameters and the first num numbers are valid) ,  led_param[6] (6 brightness parameters and the first num numbers are valid)

    // Output parameter:  None

    // Return value:  type (int):  0 means the exposure parameters setting success; -1 means the exposure parameters setting failed.

    DF_SDK_API int DfSetParamHdr(int num, int exposure_param[6]);



20.	GetParamHdr

    // Name of function:  DfGetParamHdr

    // Funciton:  Get the parameters for repeated exposures (maximum exposure number of times is 6)

    // Input parameter:  None

    // Output parameter:  num(exposure times),  exposure_param[6] (6 exposure parameters and the first num numbers are valid) ,  led_param[6] (6 brightness parameters and the first num numbers are valid)	

    // Return value:  type (int):  0 means the exposure parameters acquisition success; -1 means the exposure parameters acquisition failed.

    DF_SDK_API int DfGetParamHdr(int& num, int exposure_param[6]);

21.SetParamStandardPlaneExternal

    // Name of function:  DfSetParamStandardPlaneExternal

    // Funciton:  Set the extrinsics of the datum plane

    // Input parameter:  R(rotation matrix: 3*3),   T(Translation matrix: 3*1)

    // Output parameter:  None

    // Return value:  type (int):  0 means the parameters setting success; -1 means the parameters setting failed.

    DF_SDK_API int DfSetParamStandardPlaneExternal(float* R, float* T);

22.GetParamStandardPlaneExterna

    // Name of function:  DfGetParamStandardPlaneExternal

    // Funciton:  Get the extrinsics of the datum plane

    // Input parameter:  None

    // Output parameter:  R(rotation matrix: 3*3),   T(Translation matrix: 3*1)

    // Return value:  type (int):  0 means the parameters acquisition success; -1 means the parameters acquisition failed.

    DF_SDK_API int DfGetParamStandardPlaneExternal(float* R, float* T);

23.SetParamGenerateBrightness

	//Name of function: DfSetParamGenerateBrightness

	//Funciton:  Set the parameters for generating brightness map

	//Input parameter：model(1:Continuous exposure in sync with the fringe pattern、2：Individual luminous exposure、3：Does not glow alone exposure)、exposure(Brightness map exposure time)

	//Output parameter: None

	//Return value: type （int）:0 means the parameters acquisition success;Otherwise fail。

	DF_SDK_API int DfSetParamGenerateBrightness(int model, float exposure);

24.GetParamGenerateBrightness

	//Name of function： DfGetParamGenerateBrightness

	//Funciton： Get the generated brightness map parameters

	//Input parameter： None

	//Output parameter:model(1:Continuous exposure in sync with the fringe pattern、2：Individual luminous exposure、3：Does not glow alone exposure)、exposure(Brightness map exposure time)

	//Return value: type （int）:0 means the parameters acquisition success;Otherwise fail。

	DF_SDK_API int DfGetParamGenerateBrightness(int& model, float& exposure);

25.SetParamCameraExposure

   // Name of function:  DfSetParamCameraExposure

   // Funciton:  Set the camera exposure time

   // Input parameter:  exposure (time of the camera exposure)

   // Output parameter:  None

   // Return value:  type (int):  0 means the exposure parameters setting success; -1 means the exposure parameters setting failed.

   DF_SDK_API int DfSetParamCameraExposure(float exposure);

	
26.GetParamCameraExposure

   // Name of function:  DfGetParamCameraExposure

   // Funciton:  Get the camera exposure time

   // Input parameter:  None

   // Output parameter:  exposure (time of the camera exposure)

   // Return value:  type (int):  0 means the exposure parameters acquisition success; -1 means the exposure parameters acquisition failed.

   DF_SDK_API int DfGetParamCameraExposure(float& exposure);
  
27.SetParamMixedHdr

    // Name of function:  DfSetParamMixedHdr

    // Funciton:  Set the parameters for blending multiple exposures (maximum exposure number of times is 6)

    // Input parameter:  num (exposure times),  exposure_param[6] (6 exposure parameters and the first num numbers are valid) ,  led_param[6] (6 brightness parameters and the first num numbers are valid)

    // Output parameter:  None

    // Return value:  type (int):  0 means the exposure parameters setting success; -1 means the exposure parameters setting failed.

    DF_SDK_API int DfSetParamMixedHdr(int num, int exposure_param[6], int led_param[6]);

28.GetParamMixedHdr

   // Name of function:  DfGetParamMixedHdr

   // Funciton:  Get the parameters for blending multiple exposures (maximum exposure number of times is 6)

   // Input parameter:  None

   // Output parameter:  num(exposure times),  exposure_param[6] (6 exposure parameters and the first num numbers are valid) ,  led_param[6] (6 brightness parameters and the first num numbers are valid)

   // Return value:  type (int):  0 means the exposure parameters acquisition success; -1 means the exposure parameters acquisition failed.

   DF_SDK_API int DfGetParamMixedHdr(int& num, int exposure_param[6], int led_param[6]);

29.SetParamCameraConfidence

    // Name of function:  DfSetParamCameraConfidence

    // Funciton:  Set the camera confidence parameters

    // Input parameter:  confidence (confidence of the camera)

    //Output parameter:  None

    // Return value:  type (int):  0 means the confidence parameters setting success; -1 means the confidence parameters setting failed.

    DF_SDK_API int DfSetParamCameraConfidence(float confidence);

30.GetParamCameraConfidence

    // Name of function:  DfGetParamCameraConfidence

    // Funciton:  Get the confidence parameters of the camera

    // Input parameter:  None

    // Output parameter:  confidence (confidence of the camera)

    // Return value:  type (int):  0 means the confidence parameters acquisition success; -1 means the exposure parameters acquisition failed.

    DF_SDK_API int DfGetParamCameraConfidence(float& confidence);


31.	SetParamCameraGain

    // Name of function:  DfSetParamCameraGain

    // Funciton:  Set the gain of the camera

    // Input parameter:  gain (the gain of the camera)

    // Output parameter:  None

    // Return value:  type (int):  0 means the gain parameters setting success; -1 means the gain parameters setting failed.

    DF_SDK_API int DfSetParamCameraGain(float gain);

32.GetParamCameraGain

    // Name of function:  DfGetParamCameraGain

    // Funciton:  Get the gain of the camera

    // Input parameter:  None

    // Output parameter:  gain (the gain of the camera)

    // Return value:  type (int):  0 means the gain parameters acquisition success; -1 means the gain parameters acquisition failed.

    DF_SDK_API int DfGetParamCameraGain(float& gain);

33.SetParamSmoothing

    // Name of function:  DfSetParamSmoothing

    // Funciton:  Set the pointcloud smoothing parameters

    // Input parameter:  smoothing (0: close,  1-5: smoothness from low to high)

    // Output parameter:  None

    // Return value:  type (int):  0 means the pointcloud Smoothing parameters setting success; -1 means the pointcloud Smoothing parameters setting failed.

    DF_SDK_API int DfSetParamSmoothing(int smoothing);

34.GetParamSmoothing

    // Name of function:  DfGetParamSmoothing

    // Funciton:  Get the pointcloud smoothing parameters

    // Input parameter:  None

    // Output parameter:  smoothing (0: close,  1-5: smoothness from low to high)

    // Return value:  type (int):  0 means the pointcloud Smoothing parameters acquisition success; -1 means the pointcloud Smoothing parameters acquisition failed.

    DF_SDK_API int DfGetParamSmoothing(int& smoothing);

35.SetParamRadiusFilter

    // Name of function:  DfSetParamRadiusFilter

    // Funciton:  Set the point cloud radius filter parameters

    // Input parameter:  use (1: open, 0: close),  radius (radius),  num (effective points)

    // Output parameter:  None

    // Return value:  type (int):  0 means the radius filter parameters setting success; -1 means the radius filter parameters setting failed.

    DF_SDK_API int DfSetParamRadiusFilter(int use,float radius,int num);


36.GetParamRadiusFilter

    // Name of function:  DfGetParamRadiusFilter

    // Funciton:  Set the point cloud radius filter parameters 

    // Input parameter:  None

    // Output parameter:  use (1: open, 0: close),  radius (radius),  num (effective points)

    // Return value:  type (int):  0 means the radius filter parameters acquisition success; -1 means the radius filter parameters acquisition failed.

    DF_SDK_API int DfGetParamRadiusFilter(int& use, float& radius, int& num);

37.SetParamDepthFilter

    // Name of function:  DfSetParamRadiusFilter

    // Funciton:  Set the parameters of the depth map filter

    // Input parameter:  use (0: open, 1: close), depth_filterthreshold (filtered noise threshold)

    // Output parameter:  None

    // Return value:  type (int):  0 means the parameter setting success; else means the parameter setting failed.

    DF_SDK_API int DfSetParamDepthFilter(int use, float depth_filter_threshold);

38.GetParamDepthFilter

    // Name of function:  DfSetParamRadiusFilter

    // Funciton:  Set the parameters of the depth map filter

    // Input parameter:  use (0: open, 1: close), depth_filterthreshold (filtered noise threshold)

    // Output parameter:  None

    // Return value:  type (int):  0 means the parameter setting success; else means the parameter setting failed.

    DF_SDK_API int DfGetParamDepthFilter(int& use, float& depth_filter_threshold);

39.SetParamGrayRectify

	//Name of function： DfSetParamGrayRectify

	//Function： Set the point cloud gray compensation parameters

        //Input parameter：use(switch：1on、0 off)、radius(radius：3、5、7、9）、sigma（compensation intensity，range 0-100）

	//Output parameter： None

	//Return value： type (int):  0 means the parameter setting success; else means the parameter setting failed.

	DF_SDK_API int DfSetParamGrayRectify(int use, int radius, float sigma);

40.GetParamGrayRectify

	//Name of function： DfGetParamGrayRectify

	//Function： Obtain the point cloud gray compensation parameters

	//Input parameter：None

	//Output parameter：use(switch：1on、0 off)、radius(radius：3、5、7、9）、sigma（compensation intensity，range 0-100）

	//Return value： type (int):  0 means the parameter setting success; else means the parameter setting failed.


	DF_SDK_API int DfGetParamGrayRectify(int& use, int& radius, float& sigma);

41.SetParamOutlierFilter


    // Name of function:  DfSetParamOutlierFilter

    // Funciton:  set the outlier filter parameters

    // Input parameter:  threshold (range: 0-100)

    // Output parameter:  None

    // Return value:  type (int):  0 means the outlier filter parameters setting success; -1 means the outlier filter parameters setting failed.

    DF_SDK_API int DfSetParamOutlierFilter(float threshold);

42.GetParamOutlierFilter

    // Name of function:  DfGetParamOutlierFilter

    // Funciton:  get the outlier filter parameters

    // Input parameter:  None


    // Output parameter:  threshold (range: 0-100)

    // Return value:  type (int):  0 means the outlier filter parameters acquisition success; -1 means the outlier filter parameters acquisition failed.

    DF_SDK_API int DfGetParamOutlierFilter(float& threshold);

43.SetParamMultipleExposureModel

    // Name of function:  DfSetParamMultipleExposureModel


    // Funciton:  Set the multiple exposure mode

    // Input parameter:  model (1: HDR (Defaults),  2: repeated exposure)


    // Output parameter:  None

    // Return value:  type (int):  0 means the multiple exposure mode setting success; else means the multiple exposure mode setting failed;

    DF_SDK_API int DfSetParamMultipleExposureModel(int model);

44.SetParamRepetitionExposureNum

    // Name of function:  DfSetParamRepetitionExposureNum

    // Funciton:  Set the repetition exposure number

    // Input parameter:  num (2-10)


    // Output parameter:  None

    // Return value: type (int):  0 means the parameter setting success; else means the parameter setting failed.

    DF_SDK_API int DfSetParamRepetitionExposureNum(int num);



/**************************************************************************************/


45.ConnectNet

    //Name of function： DfConnectNet（区别于DfConnect:带注册的连接，DfConnectNet：不带注册直接连接）

    // Name of function:  DfConnect

    // Function:  Connect camera

    // Input parameter:  camera_id (Camera ip address)

    // Output parameter:  None

    // Return value:  Type(int): 0 means the connection failed; 1 means the connection success

    DF_SDK_API int DfConnectNet(const char* ip);

46.DisconnectNet

    //Name of function： DfDisconnectNet

    // Name of function:  DfDisconnect

    // Function:  Disconnect camera

    // Input parameter:  camera_id (Camera ip address)

    // Output parameter:  None

    // Return value:  Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfDisconnectNet();

47.GetCameraData

    //Name of function： DfGetCameraData


    //Function： Get a frame of camera data

    //Input parameter：None

    //Output parameter： None
 
    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetCameraData(
	short* depth, int depth_buf_size,
	unsigned char* brightness, int brightness_buf_size,
	short* point_cloud, int point_cloud_buf_size,
	unsigned char* confidence, int confidence_buf_size);

48.GetBrightness

    //Name of function： GetBrightness

    //Function： Get a brightness map data

    //Input parameter：brightness_buf_size（brightness map size sizeof(unsigned char) * width * height）

    //Output parameter：brightness

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int GetBrightness(unsigned char* brightness, int brightness_buf_size);

49.GetFocusingImage

    //Name of function： DfGetFocusingImage

    //Function： Get a focus map data

    //Input parameter：image_buf_size（brightness map size sizeof(unsigned char) * width * height）

    //Output parameter：image

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetFocusingImage(unsigned char* image, int image_buf_size);

50.GetCameraRawData01

    //Name of function： DfGetCameraRawData01

    //Function： Collect a set of phase shift maps，a total of 24 four-step phase-shift fringe patterns

    //Input parameter：raw_buf_size（Size of 24 8-bit maps）

    //Output parameter：raw

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetCameraRawData01(unsigned char* raw, int raw_buf_size);

51.GetCameraRawData02

    //Name of function： DfGetCameraRawData02

    //Function： A set of phase shift patterns were collected, 37 in total, 24 four-step phase shift fringe patterns +12 six-step phase shift fringe patterns + one brightness pattern


    //Input parameter：raw_buf_size（Size of 37 8-bitmaps）

    //Output parameter：raw

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

                                                                                                                                                             
    DF_SDK_API int DfGetCameraRawData02(unsigned char* raw, int raw_buf_size);

52.GetCameraRawDataTest 

    //Name of function： DfGetCameraRawDataTest

    //Function： Collect a set of fringe patterns 

    //Input parameter：raw_buf_size（The dimensions of a set of drawings）

    //Output parameter：raw Memory pointers

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetCameraRawDataTest(unsigned char* raw, int raw_buf_size);

53.GetCameraRawData03

    //Name of function： DfGetCameraRawData03

    //Function： A set of 31 phase shift patterns were collected, 24 four-step phase shift fringe patterns +6 six-step phase shift fringe patterns in the vertical direction + one brightness pattern

    //Input parameter：raw_buf_size（Size of 31 8-bitmaps）
 
    //Output parameter：raw

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetCameraRawData03(unsigned char* raw, int raw_buf_size);

54.DfGetCameraRawData08

    //Name of function： DfGetCameraRawData08

    //Function： A set of phase shift diagrams were collected, with a total of 14, 8 XOR codes +6 six-step phase shift fringe diagrams in vertical directions + a brightness diagram + a dark diagram


    //Input parameter：raw_buf_size（Size of 16 8-bit maps）

    //Output parameter：raw

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetCameraRawData08(unsigned char* raw, int raw_buf_size);

55.GetCameraRawData05

    //Name of function： DfGetCameraRawData05

    //Function： A set of 16 phase shift diagrams were collected, 8 xor codes +6 vertical six-step phase shift fringe diagrams + 2 black and white diagrams

    //Input parameter：raw_buf_size（Size of 16 8-bit maps）

    //Output parameter：raw

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetCameraRawData05(unsigned char* raw, int raw_buf_size);

56.GetCameraRawData06

    //Name of function： DfGetCameraRawData06
 
    //Function： A set of 18 phase shift diagrams were collected, including 10 minsw codes +6 vertical six-step phase shift fringe diagrams + 2 black and white diagrams
 
    //Input parameter：raw_buf_size（Size of 18 8-bit maps）

    //Output parameter：raw

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.
 
    DF_SDK_API int DfGetCameraRawData06(unsigned char* raw, int raw_buf_size);

57.GetCameraRawData04

    //Name of function： DfGetCameraRawData04

    //Function： A set of 19 phase shift patterns were collected, including 12 four-step phase shift fringe patterns +6 six-step phase shift fringe patterns in the vertical direction + one brightness pattern

    //Input parameter：raw_buf_size（Size of 19 8-bit maps）

    //Output parameter：raw

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetCameraRawData04(unsigned char* raw, int raw_buf_size);

58.GetCameraRawData04Repetition

    //Name of function： DfGetCameraRawData04Repetition

    //Function： A set of phase shift diagrams are collected, with a total of 13+6*repetition_count, 12 4-step phase shift fringe diagrams +6*repetition_count 6-step vertical phase shift fringe diagrams + a brightness diagram

    //Input parameter：raw_buf_size（13+6*repetition_count size of an 8-bit map）

    //Output parameter：raw
 
    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetCameraRawData04Repetition(unsigned char* raw, int raw_buf_size, int repetition_count);

59.depthTransformPointcloud

    //Name of function： depthTransformPointcloud

    //Function： Depth map to point cloud interface

    //Input parameter：depth_map（depth map）


    //Output parameter：point_cloud_map（point cloud）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int depthTransformPointcloud(float* depth_map, float* point_cloud_map);

60.undistortDepthTransformPointcloud

    //Name of function： undistortDepthTransformPointcloud

    //Function： Depth map to point cloud interface

    //Input parameter：undistort_depth_map（depth map）

    //Output parameter：point_cloud_map（point cloud）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int undistortDepthTransformPointcloud(float* undistort_depth_map, float* undistort_point_cloud_map);

61. transformPointcloud

    //Name of function： transformPointcloud

    //Function： Point cloud coordinate system conversion interface

    //Input parameter：rotate（rotation matrix）、translation（Translation Matrix）
 
    //Output parameter：point_cloud_map（point cloud）
 
    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API bool transformPointcloud(float* org_point_cloud_map, float* transform_point_cloud_map, float* rotate, float* translation);

62. transformPointcloudInv

    //Name of function： transformPointcloudInv

    //Function： Point cloud coordinate system inverse transformation (test interface)

    DF_SDK_API bool transformPointcloudInv(float* point_cloud_map, float* rotate, float* translation);

63.GetPointCloud

    //Name of function： DfGetPointCloud

    //Function： Get the point cloud interface, based on 24 four-step phase shift diagrams


    //Input parameter：point_cloud_buf_size（Point cloud memory size）

    //Output parameter：point_cloud_map（point cloud）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.


    DF_SDK_API int DfGetPointCloud(float* point_cloud, int point_cloud_buf_size);

64.GetFrame01


    //Name of function： DfGetFrame01

    //Function： Get a frame of data (brightness map + depth map) based on the phase shift map of Raw01

    //Input parameter：depth_buf_size（Depth map size）、brightness_buf_size（Luminance pattern size）

    //Output parameter：depth（depth map）、brightness（brightness map）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetFrame01(float* depth, int depth_buf_size,
	unsigned char* brightness, int brightness_buf_size);

65.GetFrameHdr

    //Name of function： DfGetFrameHdr

    //Function： Get a frame of data（brightness map+depth map），HDR mode based on Raw03 phase diagram

    //Input parameter：depth_buf_size（depth map size）、brightness_buf_size（brightness map size）


    //Output parameter：depth（depth map）、brightness（brightness map）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetFrameHdr(float* depth, int depth_buf_size,
	unsigned char* brightness, int brightness_buf_size);

66.GetFrame03

    //Name of function： DfGetFrame03

    //Function： Get a frame of data（brightness map+depth map），Based on Raw03 phase diagram

    //Input parameter：depth_buf_size（depth map size）、brightness_buf_size（brightness map size）

    //Output parameter：depth（depth map）、brightness（brightness map）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetFrame03(float* depth, int depth_buf_size,
	unsigned char* brightness, int brightness_buf_size);


67.GetFrame04

    //Name of function： DfGetFrame04

    //Function： Get a frame of data（brightness map+depth map），Based on Raw04 phase diagram

    //Input parameter：depth_buf_size（depth map size）、brightness_buf_size（brightness map size）

    //Output parameter：depth（depth map）、brightness（brightness map）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetFrame04(float* depth, int depth_buf_size,
	unsigned char* brightness, int brightness_buf_size);

68.GetFrame05

    //Name of function： DfGetFrame05

    //Function： Get a frame of data（brightness map+depth map），Compressed list-based

    //Input parameter：depth_buf_size（depth map size）、brightness_buf_size（brightness map size）

    //Output parameter：depth（depth map）、brightness（brightness map）
 
    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetFrame05(float* depth, int depth_buf_size,
	unsigned char* brightness, int brightness_buf_size);

69.GetFrame06

    //Name of function： DfGetFrame06

    //Function： Get a frame of data（brightness map+depth map），Based on Raw06 phase diagram

    //Input parameter：depth_buf_size（depth mapsize）、brightness_buf_size（brightness mapsize）

    //Output parameter：depth（depth map）、brightness（brightness map）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetFrame06(float* depth, int depth_buf_size,
	unsigned char* brightness, int brightness_buf_size);

70.GetFrame06Hdr

    //Name of function： DfGetFrame06Hdr

    //Function： Get a frame of data（brightness map+depth map），Based on Raw06 phase diagram

    //Input parameter：depth_buf_size（depth mapsize）、brightness_buf_size（brightness mapsize）

    //Output parameter：depth（depth map）、brightness（brightness map）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetFrame06Hdr(float* depth, int depth_buf_size,
	unsigned char* brightness, int brightness_buf_size);

71.GetRepetitionFrame06

    //Name of function： DfGetRepetitionFrame06

    //Function： Get a frame of data（brightness map+depth map），Based on Raw06,repetition count times

    //Input parameter：count（times of repetition）、depth_buf_size（depth map size）、brightness_buf_size（brightness map size）
 
    //Output parameter：depth（depth map）、brightness（brightness map）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetRepetitionFrame06(int count, float* depth, int depth_buf_size,
	unsigned char* brightness, int brightness_buf_size);

72.GetRepetitionFrame04

    //Name of function： DfGetRepetitionFrame04

    //Function： Get a frame of data（brightness map+depth map），Based on the Raw04 phase diagram, the 6-step phase-shift diagram is repeated count times

    //Input parameter：count（times of repetition）、depth_buf_size（depth mapsize）、brightness_buf_size（brightness mapsize）


    //Output parameter：depth（depth map）、brightness（brightness map）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.


    DF_SDK_API int DfGetRepetitionFrame04(int count, float* depth, int depth_buf_size,
	unsigned char* brightness, int brightness_buf_size);

73.GetRepetitionFrame03

    //Name of function： DfGetRepetitionFrame03

    //Function： Get a frame of data（brightness map+depth map），Based on the Raw03 phase diagram, the 6-step phase-shift diagram is repeated count times

    //Input parameter：count（times of repetition）、depth_buf_size（depth mapsize）、brightness_buf_size（brightness mapsize）

    //Output parameter：depth（depth map）、brightness（brightness map）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetRepetitionFrame03(int count, float* depth, int depth_buf_size,
	unsigned char* brightness, int brightness_buf_size);

74.GetRepetitionPhase02

    //Name of function： DfGetRepetitionPhase02

    //Function： Get a frame of data（brightness map+phase diagram），All fringe diagrams are repeated count times based on the Raw02phase diagram
 
    //Input parameter：count（times of repetition）、phase_buf_size（phase diagramsize）、brightness_buf_size（brightness mapsize）

    //Output parameter：phase_x（phase diagramx）、phase_y（phase diagramy）、brightness（brightness map）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetRepetitionPhase02(int count, float* phase_x, float* phase_y, int phase_buf_size,unsigned char* brightness, int brightness_buf_size);

75.GetCalibrationParam

    //Name of function： DfGetCalibrationParam

    //Function：Get the calibration parameter interface

    //Input parameter：None

    //Output parameter：calibration_param（calibration parameter）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetCalibrationParam(struct CameraCalibParam& calibration_param);


76.SetCalibrationParam

    //Name of function： DfSetCalibrationParam

    //Function：Set the calibration parameter interface

    //Input parameter：calibration_param（calibration parameter）

    //Output parameter：None

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfSetCalibrationParam(const struct CameraCalibParam& calibration_param);

77.SetCalibrationLookTable

    //Name of function： DfSetCalibrationLookTable

    //Function：Set the calibration parameter interface

    //Input parameter：calibration_param（calibration parameter）,rotate_x、rotate_y, rectify_r1, mapping

    //Output parameter：None

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfSetCalibrationLookTable(const struct CameraCalibParam& calibration_param, float* rotate_x,
	float* rotate_y, float* rectify_r1, float* mapping, float* mini_mapping, int width, int height);

78.SetCalibrationMiniLookTable

    //Name of function： DfSetCalibrationMiniLookTable

    //Function：Set the calibration parameter interface

    //Input parameter：calibration_param（calibration parameter）,rotate_x、rotate_y, rectify_r1, mapping
 
    //Output parameter：None

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfSetCalibrationMiniLookTable(const struct CameraCalibParam& calibration_param, float* rotate_x,
	float* rotate_y, float* rectify_r1, float* mapping);

79.GetDeviceTemperature

    //Name of function： DfGetDeviceTemperature

    //Function：Obtain device temperature

    //Input parameter：None

    //Output parameter：temperature（℃）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetDeviceTemperature(float& temperature);

80.RegisterOnDropped

    //Name of function： DfRegisterOnDropped

    //Function：Register the disconnection callback function

    //Input parameter：None

    //Output parameter：p_function（callback function）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.
 
    DF_SDK_API int DfRegisterOnDropped(int (*p_function)(void*));

81.GetCalibrationParam

    //Name of function： DfGetCalibrationParam

    //Function：Get the camera configuration parameter interface

    //Input parameter：config_param（configuration parameter）

    //Output parameter：None

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetSystemConfigParam(struct SystemConfigParam& config_param);

82.GetCalibrationParam

    //Name of function： DfGetCalibrationParam

    //Function：Set the camera configuration parameters interface

    //Input parameter：config_param（configuration parameter）

    //Output parameter：None

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfSetSystemConfigParam(const struct SystemConfigParam& config_param);

83.EnableCheckerboard

    //Name of function：  DfEnableCheckerboard

    //Function：    Turn on the light machine and project the checkerboard

    //Input parameter：None

    //Output parameter：nano temperature 1

    //Return value：  Type(int): 0 means the disconnection success; -1 means the connection failed.
 
    DF_SDK_API int DfEnableCheckerboard(float& temperature);

84.DisableCheckerboard

    //Name of function：  DfDisableCheckerboard

    //Function：    Turn off the optical projection

    //Input parameter：None

    //Output parameter：nano temperature 2

    //Return value：  Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfDisableCheckerboard(float& temperature);

85.LoadPatternData

    //Name of function：  DfLoadPatternData

    //Function：    Read the pre-set 42 projection picture data from the optical machine control board--Pattern Data

    //Input parameter：Gets the buffer size of Pattern Data、the buffer address of Pattern Data
 
    //Output parameter：Pattern Data

    //Return value：  Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfLoadPatternData(int buildDataSize, char* LoadBuffer);

86.ProgramPatternData

    //Name of function：  DfProgramPatternData

    //Function：    The Pattern Data of the DLP projection image of the optical control board is written into the FLASH of the control board by PC

    //Input parameter：The address of the packet to be written, the address of the packet read back, the size of the packet

    //Output parameter：Read back the data content

    //Return value：  Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfProgramPatternData(char* org_buffer, char* back_buffer, unsigned int pattern_size);

87.GetNetworkBandwidth

    //Name of function：  DfGetNetworkBandwidth

    //Function：    Obtain the network bandwidth of the link

    //Input parameter：None

    //Output parameter：Network bandwidth size

    //Return value：  Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetNetworkBandwidth(int& speed);


88.GetFirmwareVersion

    //Name of function：  DfGetFirmwareVersion

    //Function：    Get firmware version
 
    //Input parameter：Version number Buffer address, buffer length

    //Output parameter：version number

    //Return value：  Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetFirmwareVersion(char* pVersion, int length);

89.SelfTest

    //Name of function：  DfSelfTest
 
    //Function：    Get self-test results

    //Input parameter：Self-check result buffer address, buffer length

    //Output parameter：Self-check result

    //Return value：  Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfSelfTest(char* pTest, int length);

90.GetCameraVersion

    //Name of function：  DfGetCameraVersion

    //Function：    Get camera model

    //Input parameter：None

    //Output parameter：model（800、1800）

    //Return value：  Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetCameraVersion(int& version);

91.GetProjectVersion

    //Name of function：  DfGetProjectVersion

    //Function：    Get camera model

    //Input parameter：None

    //Output parameter：model（3010、4710）

    //Return value：  Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetProjectorVersion(int& version);

92.SetParamOffset

    //Name of function： DfSetParamOffset

    //Function： Set compensation parameters

    //Input parameter：offset(compensation value)

    //Output parameter： None

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfSetParamOffset(float offset);

93.GetParamOffset

    //Name of function： DfGetParamOffset

    //Function： Get compensation parameters

    //Input parameter：None

    //Output parameter：offset(compensation value)

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetParamOffset(float& offset);

94.SetParamBilateralFilter

    //Name of function： DfSetParamBilateralFilter

    //Function： Set bilateral filtering parameters

    //Input parameter： use（switch：1 on、0 off）、param_d（smoothing factor：3、5、7、9、11）

    //Output parameter： None

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfSetParamBilateralFilter(int use, int param_d);

95.GetParamBilateralFilter

    //Name of function： DfGetParamBilateralFilter

    //Function： Get mixed multiple exposure parameters (maximum 6 exposures)

    //Input parameter： None

    //Output parameter： use（switch：1 on、0 off）、param_d（smoothing factor：3、5、7、9、11）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetParamBilateralFilter(int& use, int& param_d);

96.SetAutoExposure

    //Name of function：  DfSetAutoExposure

    //Function：    Get camera model

    //Input parameter：flag(1:roi model、2：board model)

    //Output parameter：exposure、led

    //Return value：  Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfSetAutoExposure(int flag, int& exposure, int& led);

97.GetProjectorTemperature

    //Name of function： DfGetProjectorTemperature

    //Function： The optical machine temperature is obtained and expressed in the form of the resistance value of the thermistor

    //Input parameter：None

    //Output parameter：Resistance，kΩ

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetProjectorTemperature(float& temperature);

98.CaptureRepetitionData

     //Name of function： DfCaptureRepetitionData

    //Function： Collect a frame of data and block until the return state

    //Input parameter：repetition_count（times of repetition）、 exposure_num（exposure times）：Set a value of 1 for single exposure, greater than 1 for 
multi-exposure mode (specific parameters are set in the camera gui)
 
    //Output parameter： timestamp(timestamp)

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfCaptureRepetitionData(int repetition_count, int exposure_num, char* timestamp);

99.GetTestFrame01

    //Name of function： DfGetTestFrame01

    //Function： Send a set of Raw01 phase shift plots to firmware and reconstruct the data back to a frame（brightness map+depth map）

    //Input parameter：raw（Phase shift map address）、raw_buf_size（Phase shift map size）、 depth_buf_size（depth mapsize）、brightness_buf_size （brightness mapsize）

    //Output parameter：depth（depth map）、brightness（brightness map）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetTestFrame01(unsigned char* raw, int raw_buf_size, float* depth, int depth_buf_size,
	unsigned char* brightness, int brightness_buf_size);

100.SetParamReflectFilter

    //Name of function： DfSetParamReflectFilter

    //Function： Set filtering parameters for point cloud radius

    //Input parameter：use(switch：1 on、0 off) 

    //Output parameter： None

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfSetParamReflectFilter(int use);

101.GetParamReflectFilter

    //Name of function： DfGetParamReflectFilter

    //Function： Set point cloud smoothing parameters

    //Input parameter：None

    //Output parameter：use(switch：1 on、0 off)

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetParamReflectFilter(int& use);

102.SetBoardInspect

    //Name of function： DfSetBoardInspect

    //Function： Set up calibration board detection

    //Input parameter：enable(switch) 

    //Output parameter： None

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfSetBoardInspect(bool enable);

103.GetProductInfo

    //Name of function： DfGetProductInfo

    //Function： Set up calibration board detection

    //Input parameter：info(message)，lenth(message length) 

    //Output parameter： None

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetProductInfo(char* info, int length);

104.GetFrameStatus

    //Name of function： DfGetFrameStatus

    //Function： Gets the current frame data status

    //Input parameter：None

    //Output parameter： status（status code）

    //Return value： Type(int): 0 means the disconnection success; -1 means the connection failed.

    DF_SDK_API int DfGetFrameStatus(int& status);
 

 ## Routine

Please see the example.cpp

Property description

        // Structure of the camera calibration parameter

struct CalibrationParam

{

	double intrinsic[3*3];   // Camera Intrinsics

	double extrinsic[4*4];  // Camera Extrinsic

	//Camera Distortion // <k1,k2,p1,p2,k3,k4,k5,k6,s1,s2,s3,s4> Only use 5 parameters for now

	double distortion[1*12];

};


// Structure of the basic device information

struct DeviceBaseInfo

{

	char mac[64];  // Camera Intrinsics

	char ip[64];  // Camera Extrinsic

};

## Error Code

Error Code | Value | Description
-- | -- | --
DF_SUCCESS | 0 | Success
DF_FAILED | -1 | Failed
DF_UNKNOWN | -2 | Unknown command
DF_BUSY | -3 | Camera occupied
DF_NOT_CONNECT | -4 | Camera unconnected
DF_ERROR_NETWORK | -5 | Network Error
DF_ERROR_2D_CAMERA | -6 | 2D camera error
DF_ERROR_INVALID_PARAM | -7 | Invalid parameter
DF_ERROR_LIGHTCRAFTER_SET_MODEL | -8 | Light engine projection mode setting error
DF_ERROR_LIGHTCRAFTER_SET_TRIGGEROUT | -9 | Light engine trigger mode setting error
DF_ERROR_LIGHTCRAFTER_SET_CURRENT | -10 | Light engine brightness setting error
DF_ERROR_LIGHTCRAFTER_SET_PATTERN_ORDER | -11 | Light engine stripe setting error
DF_ERROR_CAMERA_STREAM | -12 | Camera operation flow error
DF_ERROR_CAMERA_GRAP | -13 | Camera captures images error
DF_FRAME_CAPTURING | -14 | Camera is capturing data
