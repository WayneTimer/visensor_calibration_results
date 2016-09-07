# visensor_calibration_results

Use kalibr to calibrate visensor.
Step:
```
1. Make sure visensor config is 20HZ image rate and 200HZ imu rate, agc and aec enabled
2. roslaunch visensor_node dense.launch
3. rosbag record -a
4. rosrun kalibr kalibr_calibrate_cameras --target checkerboard.yaml --bag <bagpath> --models pinhole-radtan pinhole-radtan --topics /cam0/image_raw /cam1/image_raw
5. rosrun kalibr kalibr_calibrate_imu_camera --bag <bagpath> --cam camchain-hometimerROS_bags<bagname>.yaml --imu imu.yaml --target checkerboard.yaml
6. copy camchain-imucam-hometimerROS_bags<bagname>.yaml to ~/catkin_ws/src/visensor_tools/visensor_calibration_flasher/camchain-imucam-example.yaml
7. roslaunch visensor_calibration_flasher flash_sensor.launch
```
