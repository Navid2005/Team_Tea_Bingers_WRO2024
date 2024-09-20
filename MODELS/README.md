This contains 3D models and sketches during the development of the robots design.

COCO MODEL 1.0 DESCRIPTION:
The first iteration of the robot was rectangular in shape with a bearing and bar based steering system controlled by a servo motor. 2 Arduino Uno's were conceptualized to control both image processing and other IOT functions separately, they would communicate via an I2C protocol,moreover a toggle switch was used to power the Arduino board and another push button switch was going to be used to allow power to the L298N Motor driver to move the robot. IR sensors on the front and back were thought up to be used for the parallel parking segment of the obstacle challenge. 2 HC-SR04 distance sensor on either side would help determine when to initialize a steering movement. The OLED screen was added to display battery life and our team logo. An ESP32 camera would be used for object detection during the Obstacle course round. Finally, an MPU6050 acts as lap counter due to its built in Accelerometer and gyroscope capabilities, allowing us to stop after 3 laps and stay within our starting segment.

FRONT VIEW:
![Front view of Coco V1 0](https://github.com/user-attachments/assets/96f5fd17-7392-4108-9b9c-aa5fdae903a7)

TOP VIEW: 
![Complete top view of coco V1 0](https://github.com/user-attachments/assets/c93a4ede-f2cd-42f5-aff3-90cf2c98e044)

SIDE VIEW:
![Side view of Coco V1 0](https://github.com/user-attachments/assets/d2acbdb2-c002-4fc7-8752-a1a291fd1f67)
