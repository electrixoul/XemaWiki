Interface Document of XEMA 

Version Record

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

interface description

Interfaces (1-33) are in the header file of open_cam3d_sdk.h.

Interfaces (34,35) are in the header file of enumerate.h.

Error Codes are defined in camera_status.h.

1. Connect

int DfConnect(const char* camera_id);

        // Name of function:  DfConnect

        // Function:  Connect camera

        // Input parameter:  camera_id (Camera ip address)

        // Output parameter:  None

        // Return value:  Type(int): 0 means the connection failed; 1 means the connection success

2. Disconnect

int DfDisconnect(const char* camera_id);

        // Name of function:  DfDisconnect

        // Function:  Disconnect camera

        // Input parameter:  camera_id (Camera ip address)

        // Output parameter:  None

        // Return value:  Type(int): 0 means the disconnection success; -1 means the connection failed.

3. Get camera resolution

int DfGetCameraResolution(int* width, int* height);

        // Name of function:  DfGetCameraResolution

        // Function:  Get the camera resolution

        // Input parameter:  None

        // Output parameter:   width(image width),  height(image height)

        // Return value:  Type(int): 0 means the parameter acquisition success; -1 means the parameter acquisition failed.

4. Capture camera data

int DfCaptureData(int exposure_num, char* &timestamp);

        // Name of function:  DfCaptureData

        // Function:  Collect point cloud data and block until the result is returned

        // Input parameter:  Exposure_num (Exposure times (repeated exposure when >1) ) 

        // Output parameter:  timestamp (value of timestamp)

        // Return value:  Type(int): 0 means the point cloud acquisition success; -1 means the point cloud acquisition failed.

5. Get Depth Data

int DfGetDepthData(unsigned short* depth);

        // Name of function:  DfGetDepthData

	// Funciton:  Get depth map data

	// Input parameter:  None

	// Out parameter:  depth (depth map)

        // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

The parameter is the data pointer corresponding to the image and the caller needs to apply for memory space in advance according to the return result of function DfGetCameraResolution.

The data will be arranged in the order of H (row)/W (column)/C (channel) in the memory.

6. Get HeightMap Data

         // Name of function:  DfGetHeightMapData

         // Funciton:  Get height map data

         // Input parameter:  None

         // Onput parameter:  height_map (data of height map)

         // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

The parameter is the data pointer corresponding to the image and the caller needs to apply for memory space in advance according to the return result of function DfGetCameraResolution.

The data will be arranged in the order of H (row)/W (column)/C (channel) in the memory.

7. Get Brightness Data

int DfGetBrightnessData(unsigned short* depth);

        // Name of function:  DfGetBrightnessData

	// Funciton:  Get brightness data

	// Input parameter:  None

	// Onput parameter:  brightness(data of brightness map)

        // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

The parameter is the data pointer corresponding to the image and the caller needs to apply for memory space in advance according to the return result of function DfGetCameraResolution.

The data will be arranged in the order of H (row)/W (column)/C (channel) in the memory.

8. Get Standard Plane Param

int DfGetStandardPlaneParam(float* R,float* T);

        // Name of function:  DfGetStandardPlaneParam

        // Funciton:  Get datum plane parameters

        // Input parameter:  None

        // Output parameter:  R(rotation matrix: 3*3),   T(Translation matrix: 3*1)

        // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

9. Get Height Map Data Base Param

int DfGetHeightMapDataBaseParam(float* R, float* T, float* height_map);

        // Name of function:  DfGetHeightMapDataBaseParam

        // Funciton:  Get the height map corrected to the datum plane

        // Input parameter:  R(rotation matrix: 3*3),   T(Translation matrix: 3*1)

        // Output parameter:  height_map (data of height map)

        // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

10. Get Pointcloud Data

int DfGetPointcloudData(float* point_cloud);	

        // Name of function:  DfGetPointcloudData

	// Funciton:  Get the data of point cloud (depth map to point cloud)

	// Input parameter:  None

	// Output parameter:  point_cloud (data of point cloud)

        // Return value:  type (int):  0 means the data acquisition success; -1 means the data acquisition failed.

The parameter is the data pointer corresponding to the image and the caller needs to apply for memory space in advance according to the return result of function DfGetCameraResolution.

The data will be arranged in the order of H (row)/W (column)/C (channel) in the memory.

11. Get Calibration Parameters

int DfGetCalibrationParam(struct CalibrationParam* calibration_param);
 
        // Name of function:  DfGetCalibrationParam

        // Funciton:  Get the camera calibration parameters

        // Input parameter:  None

        // Output parameter:  calibration_param (Camera calibration parameter structure)

        // Return value:  type (int):  0 means the calibration parameters acquisition success; -1 means the data acquisition failed.

12. Set Led Current Parameters

int DfSetParamLedCurrent(int led);

        // Name of function:  DfSetParamLedCurrent

        // Funciton:  Set the current of LED

        // Input parameter:  led (current)

        // Output parameter:  None

        // Return value:  type (int):  0 means the parameter setting success; -1 means the parameter setting failed.

13. Get Led Current Parameters

int DfGetParamLedCurrent(int led);

	// Name of function:  DfGetParamLedCurrent

	// Funciton:  Get the current of LED

	// Input parameter:  None

	// Output parameter:  led (current)

        // Return value:  type (int):  0 means the parameter acquisition success; -1 means the parameter acquisition failed.

14. Set Hdr Parameters

int DfSetParamHdr(int num, int exposure_param[6], int led_param[6]);

	// Name of function:  DfSetParamHdr

	// Funciton:  Set the parameters for repeated exposures (maximum exposure number of times is 6)

	// Input parameter:  num(exposure times),  exposure_param[6] (6 exposure parameters and the first num numbers are valid) ,  led_param[6] (6 brightness parameters and the first num numbers are valid)

	// Output parameter:  None

        // Return value:  type (int):  0 means the exposure parameters setting success; -1 means the exposure parameters setting failed.

15. Get Hdr Parameters

int DfGetParamHdr(int& num, int exposure_param[6], int led_param[6]);

	// Name of function:  DfGetParamHdr

	// Funciton:  Get the parameters for repeated exposures (maximum exposure number of times is 6)

	// Input parameter:  None

	// Output parameter:  num(exposure times),  exposure_param[6] (6 exposure parameters and the first num numbers are valid) ,  led_param[6] (6 brightness parameters and the first num numbers are valid)	

        // Return value:  type (int):  0 means the exposure parameters acquisition success; -1 means the exposure parameters acquisition failed.

16. Set Standard Plane Parameters

int DfSetParamStandardPlaneExternal(float* R, float* T);

	// Name of function:  DfSetParamStandardPlaneExternal

	// Funciton:  Set the extrinsics of the datum plane

        // Input parameter:  R(rotation matrix: 3*3),   T(Translation matrix: 3*1)

	// Output parameter:  None

        // Return value:  type (int):  0 means the parameters setting success; -1 means the parameters setting failed.

17. Get Standard Plane Parameters

int DfGetParamStandardPlaneExternal(float* R, float* T);

	// Name of function:  DfGetParamStandardPlaneExternal

	// Funciton:  Get the extrinsics of the datum plane

	// Input parameter:  None

        // Output parameter:  R(rotation matrix: 3*3),   T(Translation matrix: 3*1)

	// Return value:  type (int):  0 means the parameters acquisition success; -1 means the parameters acquisition failed.

18. Set Camera Exposure Parameters

int DfSetParamCameraExposure(float exposure);

	// Name of function:  DfSetParamCameraExposure

	// Funciton:  Set the camera exposure time

	// Input parameter:  exposure (time of the camera exposure)

	// Output parameter:  None

	// Return value:  type (int):  0 means the exposure parameters setting success; -1 means the exposure parameters setting failed.

19. Get Camera Exposure Parameters

int DfGetParamCameraExposure(float& exposure);


	// Name of function:  DfGetParamCameraExposure

	// Funciton:  Get the camera exposure time

	// Input parameter:  None

	// Output parameter:  exposure (time of the camera exposure)

	// Return value:  type (int):  0 means the exposure parameters acquisition success; -1 means the exposure parameters acquisition failed.

20. Get Mixed Hdr Parameters

int DfGetParamMixedHdr(int& num, int exposure_param[6], int led_param[6]);


	// Name of function:  DfGetParamMixedHdr

	// Funciton:  Get the parameters for blending multiple exposures (maximum exposure number of times is 6)

	// Input parameter:  None

	// Output parameter:  num(exposure times),  exposure_param[6] (6 exposure parameters and the first num numbers are valid) ,  led_param[6] (6 brightness parameters and the first num numbers are valid)
	
        // Return value:  type (int):  0 means the exposure parameters acquisition success; -1 means the exposure parameters acquisition failed.

21. Set Camera Confidence Parameters

int DfSetParamCameraConfidence(float confidence);


        // Name of function:  DfSetParamCameraConfidence

        // Funciton:  Set the camera confidence parameters

        // Input parameter:  confidence (confidence of the camera)

        //Output parameter:  None

        // Return value:  type (int):  0 means the confidence parameters setting success; -1 means the confidence parameters setting failed.

22. Set Mixed Hdr Parameters

int DfSetParamMixedHdr(int num, int exposure_param[6], int led_param[6]);

        // Name of function:  DfSetParamMixedHdr

        // Funciton:  Set the parameters for blending multiple exposures (maximum exposure number of times is 6)

        // Input parameter:  num (exposure times),  exposure_param[6] (6 exposure parameters and the first num numbers are valid) ,  led_param[6] (6 brightness parameters and the first num numbers are valid)

        // Output parameter:  None

        // Return value:  type (int):  0 means the exposure parameters setting success; -1 means the exposure parameters setting failed.

23. Get Camera Confidence Parameters

int DfGetParamCameraConfidence(float& confidence);

        // Name of function:  DfGetParamCameraConfidence

        // Funciton:  Get the confidence parameters of the camera

        // Input parameter:  None

        // Output parameter:  confidence (confidence of the camera)

        // Return value:  type (int):  0 means the confidence parameters acquisition success; -1 means the exposure parameters acquisition failed.

24. Set Camera Gain Parameters

int DfSetParamCameraGain(float gain); 

        // Name of function:  DfSetParamCameraGain

        // Funciton:  Set the gain of the camera

        // Input parameter:  gain (the gain of the camera)

        // Output parameter:  None

        // Return value:  type (int):  0 means the gain parameters setting success; -1 means the gain parameters setting failed.

25. Get Camera Gain Parameters

int DfGetParamCameraGain(float& gain);

        // Name of function:  DfGetParamCameraGain

        // Funciton:  Get the gain of the camera

        // Input parameter:  None

        // Output parameter:  gain (the gain of the camera)

        // Return value:  type (int):  0 means the gain parameters acquisition success; -1 means the gain parameters acquisition failed.

26. Set Pointcloud Smoothing Parameters

int DfSetParamSmoothing(int smoothing);

        // Name of function:  DfSetParamSmoothing

        // Funciton:  Set the pointcloud smoothing parameters

        // Input parameter:  smoothing (0: close,  1-5: smoothness from low to high)

        // Output parameter:  None

        // Return value:  type (int):  0 means the pointcloud Smoothing parameters setting success; -1 means the pointcloud Smoothing parameters setting failed.

27. Get Pointcloud Smoothing Parameters

int DfGetParamSmoothing(int& smoothing);

        // Name of function:  DfGetParamSmoothing

        // Funciton:  Get the pointcloud smoothing parameters
        // Input parameter:  None

        // Output parameter:  smoothing (0: close,  1-5: smoothness from low to high)

        // Return value:  type (int):  0 means the pointcloud Smoothing parameters acquisition success; -1 means the pointcloud Smoothing parameters acquisition failed.

28. Set Radius Filter Parameters

int DfSetParamRadiusFilter(int use,float radius,int num);

        // Name of function:  DfSetParamRadiusFilter

        // Funciton:  Set the point cloud radius filter parameters

        // Input parameter:  use (1: open, 0: close),  radius (radius),  num (effective points)

        // Output parameter:  None

        // Return value:  type (int):  0 means the radius filter parameters setting success; -1 means the radius filter parameters setting failed.

29. Get Radius Filter Parameters

int DfGetParamRadiusFilter(int& use, float& radius, int& num);

        // Name of function:  DfGetParamRadiusFilter

        // Funciton:  Set the point cloud radius filter parameters 

        // Input parameter:  None

        // Output parameter:  use (1: open, 0: close),  radius (radius),  num (effective points)

        // Return value:  type (int):  0 means the radius filter parameters acquisition success; -1 means the radius filter parameters acquisition failed.

30. Set Outlier Filter Parameters

int DfSetParamOutlierFilter(float threshold);

        // Name of function:  DfSetParamOutlierFilter

        // Funciton:  set the outlier filter parameters

        // Input parameter:  threshold (range: 0-100)

        // Output parameter:  None

        // Return value:  type (int):  0 means the outlier filter parameters setting success; -1 means the outlier filter parameters setting failed.

31. Get Outlier Filter Parameters

int DfGetParamOutlierFilter(float& threshold);	

        // Name of function:  DfGetParamOutlierFilter

        // Funciton:  get the outlier filter parameters

        // Input parameter:  None

        // Output parameter:  threshold (range: 0-100)

        // Return value:  type (int):  0 means the outlier filter parameters acquisition success; -1 means the outlier filter parameters acquisition failed.

32. Set Multiple Exposure Model Parameters

int DfSetParamMultipleExposureModel(int model);

        // Name of function:  DfSetParamMultipleExposureModel

        // Funciton:  Set the multiple exposure mode

        // Input parameter:  model (1: HDR (Defaults),  2: repeated exposure)

        // Output parameter:  None

        // Return value:  type (int):  0 means the multiple exposure mode setting success; else means the multiple exposure mode setting failed;

33. Set Repetition Exposure Num Parameters

int DfSetParamRepetitionExposureNum(int num);

        // Name of function:  DfSetParamRepetitionExposureNum

        // Funciton:  Set the repetition exposure number

        // Input parameter:  num (2-10)

        // Output parameter:  None

        // Return value: type (int):  0 means the parameter setting success; else means the parameter setting failed.

34. Update Device List

int DfUpdateDeviceList(int& device_num);
	
        // Name of function:  DfUpdateDeviceList

        // Funciton:  Get the number of connectable devices

        // Input parameter:  device_num (the number of connectable devices)

        // Output parameter:  None

        // Return value:  type (int):  0 means the connection success; else means the parameter connection failed.

35. Get All Device Base Info

int DfGetAllDeviceBaseInfo(DeviceBaseInfo* pDeviceInfo, int* pBufferSize);

        // Name of function:  DfGetAllDeviceBaseInfo

        // Funciton:  Get the basic information of the device

        // Input parameter:  pDeviceInfo (information of the device),  pBufferSize (memory size of the device structure)

        // Output parameter:  None

        // Return value:  type (int):  0 means the information acquisition success; else means the information acquisition failed.

36. Set Depth Filter Parameters

int DfSetParamDepthFilter(int use, float depth_filter_threshold);

        // Name of function:  DfSetParamRadiusFilter

        // Funciton:  Set the parameters of the depth map filter

        // Input parameter:  use (0: open, 1: close), depth_filterthreshold (filtered noise threshold)

        // Output parameter:  None

        // Return value:  type (int):  0 means the parameter setting success; else means the parameter setting failed.

37. Get Depth Filter Parameters

int DfGetParamDepthFilter(int& use, float& depth_filter_threshold);

        // Name of function:  DfSetParamRadiusFilter

        // Funciton:  Get the parameters of the depth map filter

        // Input parameter:  None

        // Output parameter:  use (0: open, 1: close), depth_filterthreshold (filtered noise threshold)

        // Return value: type (int):  0 means the parameter set success; else means the parameter set failed.

 Routine

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

Error Code

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
