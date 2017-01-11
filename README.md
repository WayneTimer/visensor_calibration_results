# visensor_calibration_results

Use kalibr to calibrate visensor.
Step:
```
1. Make sure visensor config is 20HZ image rate and 200HZ imu rate, agc and aec enabled
2. rosrun visensor_node visensor_node
3. rosbag record -a
4. rosrun kalibr kalibr_calibrate_cameras --target checkerboard.yaml --bag <bagpath> --models pinhole-radtan pinhole-radtan --topics /cam0/image_raw /cam1/image_raw
5. rosrun kalibr kalibr_calibrate_imu_camera --bag <bagpath> --cam camchain-hometimerROS_bags<bagname>.yaml --imu imu.yaml --target checkerboard.yaml
6. cp camchain-imucam-hometimerROS_bags<bagname>.yaml ~/catkin_ws/src/visensor_tools/visensor_calibration_flasher/camchain-imucam-example.yaml
7. roslaunch visensor_calibration_flasher flash_sensor.launch
```

Use MEI/PINHOLE to cali:
```
1. Replace calib.launch  
2. roslaunch camera_calibration_frontend calib.launch  
3. Save the images, and extract from /tmp/...tar.gz  
4. git clone ***/camera_model  
5. rosrun camera_model Calibration -w 11 -h 8 -s 70 -i <images_path>  
(Default is mei, if use pinhole: rosrun camera_model Calibration --camera-model pinhole -w 11 -h 8 -s 70 -i <images_path>)
```
