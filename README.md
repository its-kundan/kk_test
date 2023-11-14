
# Documentation By Kundan Kumar.

## Task 0

Installing software and basics learning.

## Task 1 A ( PID Tune )

### The aim of this task is to build a PID control system to stabilise the Swift Drone at any given position in a simulation environment in Gazebo.

#### Problem Statement

The task is to build a PID controller for controlling position (x,y,z) of the swift drone in Gazebo world.

The PID controller will be a closed loop controller with real time position of the swift drone being fed-back to the controller as a feedback.

The output of the controller will be commands to the swift drone as angle-setpoints which the swift drone is supposed to tilt at.

The PID controller will be written as a rosnode written in python programming language.

After the PID controller is build and tuned successfully, the swift drone should be able to move and stabilise at the given setpoint [2,2,20] in the gazebo environment and stay within the error range of ±0.2m in all the coordinates.

#### Installation
- Create a catkin workspace

```
cd
mkdir catkin_ws/src -p
cd catkin_ws
catkin init
```
- Build your workspace
```
cd ~/catkin_ws
catkin build
```
- Each time you build your workspace, you need to source setup.bash file from the catkin_ws/devel folder. Instead of doing this manually, let us add a line in .bashrc.
```
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
```
- Now clone the luminosity_drone and other ros packages form GitHub

```
cd ~/catkin_ws/src 
git clone https://github.com/eYantra-Robotics-Competition/luminosity_drone --recursive
git clone https://github.com/simmubhangu/pid_tune
```
- Install dependencies
```
sudo apt install python-tk ros-noetic-octomap-msgs ros-noetic-octomap-ros ros-noetic-mavlink libgoogle-glog-dev ros-noetic-plotjuggler-ros 
```
- Now build your workspace
```
cd ~/catkin_ws
catkin build
source ~/.bashrc
```

#### Procedure

- Launch the Gazebo world containing the swift drone and the overhead camera by typing the following command:

```
roslaunch luminosity_drone task_1.launch
```
- Read the boiler-plate python program position_hold.py given in the catkin_ws/src/luminosity_drone/luminosity_drone/scripts folder thoroughly and complete the script to build the PID controller.
- Tune the PID controller to optimise the performance of the swift drone and achieve the desired output. After tuning, fix the P, I and D gains in your python script.
- To launch the GUI slider for tuning PID values, run the following command:
```
rosrun pid_tune pid_tune_drone.py
```
- To launch Plotjuggler for visualizing ros topics, run the following command:
```
roslaunch plotjuggler_ros plotjuggler.launch
```

#### Submission

- Step 1: Implement the PID controller and complete the python script for position hold.

- Step 2: Tune the P, I and D values as shown in the video for roll, pitch and throttle using the GUI slider. After you are confident with your P, I and D gains, fix them in your code and make sure you multiply the constants that were used to scale down the gains in the call back function. For eg, if your P gain in GUI slider was 1000, and your multiplication factor in the callback function is 0.06, then the effective P gain is 60, so hardcode this gain in the script in the variables so that just by running the code, the PID controller starts. Do this for roll, pitch and throttle.

- Step 3: Now you need to record your submission, a tool named rosbag helps to record rostopics just as a video. When you feel confident with the performance of your PID controller and you are ready to record the submission, use another launch file which will run the same things as in task_1.launch as well as start the position_controller.py and a node to record rosbag after 5 seconds delay so that gazebo starts and drone is spawned.Use this launch file to implement the task and record a bag file for 1 minute i.e. 60 seconds
- 
```
roslaunch luminosity_drone task_1_submission.launch
```

Step 4: This will generate a bag file named position_hold_<date_time>.bag in the scripts folder, change the name to LD_<team_id>_position_hold.bag, you need to make a zip file containing this bag file and the python script, change the name of python script to LD_<team_id>_position_hold.py.
NOTE: The zip should contain only 2 files in the root directory, DO NOT make a folder and then zip, directly zip the two files. You can use this command to zip the file. Use this command only after you have renamed both the files. replace <team_id> with your team id, for eg. if your team id is 1234, then the file names should be LD_1234_position_hold.bag and LD_1234_position_hold.py.

```
zip -r LD_<team_id>.zip LD_<team_id>_position_hold.bag LD_<team_id>_position_hold.py
```

This should be the structure of zip file
`|__LD_1234.zip
… |__LD_1234_position_hold.bag
… |__LD_1234_position_hold.py`

Step 5: Submit this zip file on the portal in the place of Task 1A and check your score.

######  For zipping multiple files 
```
zip -r folder_name.zip file1.bag file2.py
```


## TASK 1B LED Detection and Analyzation

The aim of this task is to detect the no. of LEDs in a given image and find the centroid coordinates and area of each LED.

resources
links https://docs.opencv.org/4.5.0/da/df6/tutorial_py_table_of_contents_setup.html
https://docs.opencv.org/4.5.0/dc/d4d/tutorial_py_table_of_contents_gui.html
https://docs.opencv.org/4.5.0/d7/d16/tutorial_py_table_of_contents_core.html
https://docs.opencv.org/4.5.0/d2/d96/tutorial_py_table_of_contents_imgproc.html
https://docs.opencv.org/4.5.0/d7/d4d/tutorial_py_thresholding.html




Aim:
The aim of this task is to detect the no. of LEDs in a given image and find the centroid coordinates and area of each LED.
Prerequisites
It is presumed that you have successfully gone through the image processing resources provided in Task1. Also this task involves writing programs in Python programming language, so get acquainted with the basics of Python and OpenCV libraries for Python.
Installations
Before proceeding further, you need to install the some packages. To do that, follow these commands:

```
Installing scikit-image
```


```
pip3 install scikit-image
```
Installing imutils

```
pip3 install imutils
```
### Problem Statement
- The task is to detect the no. of LEDs in the given image

- Mark the LEDs

- Calculate the centroid coordinates and area of each LED

- After this, save the no. of LEDs detected, the centroid coordinates and area of each LED onto a .txt file

- Finally save the processed image with LEDs marked on it to a .png file

#### Procedure
- Carefully read the boiler-plate python program led_detection.py given in the catkin_ws/src/luminosity_drone/luminosity_drone/scripts folder thoroughly and complete the script to process the image given in the same folder.

- The script should be able to generate an output image (Figure 1) from a given sample image (Figure 2)

sample.png
Figure 1: sample.png

sample_output.png
Figure 2: sample_output.png
Your code should be able to generate a .txt file containing the no. of LEDs detected, the centroid coordinates and area of each of the detected LEDs.
sample.txt
Figure 1: sample.txt
#### Submission instructions
- Step 1: Rename the .txt file to LD_<team_id>_led_detection_results.txt

- Step 2: Rename the .pngfile to LD_<team_id>_led_detection_results.png

- Step 3: Create a zip file containing this text file, image file and the python script, change the name of python script to LD_<team_id>_led_detection.py.
NOTE: The zip should contain only 3 files in the root directory, DO NOT make a folder and then zip, directly zip the three files. You can use this command to zip the file. Use this command only after you have renamed both the files. replace <team_id> with your team id, for eg. if your team id is 1234, then the file names should be LD_1234_led_detection_results.txt, LD_1234_led_detection_results.png and LD_1234_led_detection.py.


zip -r LD_<team_id>.zip LD_<team_id>_led_detection_results.txt LD_<team_id>_led_detection_results.png LD_<team_id>_led_detection.py
This should be the structure of zip file
|__LD_1234.zip
… |__LD_1234_led_detection_results.txt
… |__LD_1234_led_detection_results.png
… |__LD_1234_led_detection.py

Step 4: Submit this zip file on the portal in the place of Task 1B and check your score.
Deadline





## TASK 2B Waypoint Navigation using Swift drone
#### Aim:
The aim of this task is to write a wrapper over the existing PID control system, written in Task 1 to fly the Swift drone through a list of set points in the simulation environment in Gazebo.
##### Prerequisites
It is presumed that you have successfully completed Task 1 and the prerequisites of the same. No new resources, apart from task 1 are needed for this task, however do not limit yourself with the same, the internet is a vast ocean of knowledge, make use of it!
Installations
We’ve pushed new code to the exisiting package. You simply need to pull it and run catkin build

```
cd ~/catkin_ws/src/luminosity_drone
git pull origin ros_pkg --recurse-submodules
cd ~/catkin_ws
catkin build
```
Problem Statement
The Swift drone should move through each set point in the gazebo environment

Takeoff
[0, 0, 23]
[2, 0, 23]
[2, 2, 23]
[2, 2, 25]
[-5, 2, 25]
[-5, -3, 25]
[-5, -3, 21]
[7, -3, 21]
[7, 0, 21]
[0, 0, 19]
A waypoint will be considered a success if the drone gets within the error range of ±0.2m in all the coordinate axis for even one instance.

#### Procedure
Launch the Gazebo world containing the swift drone and the overhead camera by typing the following command

```
roslaunch luminosity_drone task_2a.launch
```
Make a new python script waypoint_navigation.py in the catkin_ws/src/luminosity_drone/luminosity_drone/scripts folder and complete the script to fly the drone through the mentioned set points.

Potentially use the PID values from task 1 to achieve optimal performance of the swift drone flight in your python script.

Follow the recording and submission instructions to submit your task

#### Recording and Submission instructions
- Step 1: Use the PID controller and complete the python script for flying the swift drone.

- Step 2: Tune the P, I and D values from task 1 (or tune again if needed) for roll, pitch and throttle appropriately in your code. And add in a wrapper over your code to fly the swift drone through the mentioned setpoints and finally stabilize on the last setpoint.

- Step 3: Now you need to record your submission, a tool named rosbag helps to record rostopics just as a video. When you feel confident with the performance of your PID controller and you are ready to record the submission, use another launch file which will run the same things as in task_1.launch as well as start the waypoint_navigation.py and a node to record rosbag after 10 seconds delay so that gazebo starts and drone is spawned. Use this launch file to implement the task and record a bag file for 2 minute i.e. 120 seconds

roslaunch luminosity_drone task_2a_submission.launch
- Step 4: This will generate a bag file named waypoint_navigation_<date_time>.bag in the scripts folder, change the name to LD_<team_id>_waypoint_navigation.bag, you need to make a zip file containing this bag file and the python script, change the name of python script to LD_<team_id>_waypoint_navigation.py.
NOTE: The zip should contain only 2 files in the root directory, DO NOT make a folder and then zip, directly zip the two files. You can use this command to zip the file. Use this command only after you have renamed both the files. replace <team_id> with your team id, for eg. if your team id is 1234, then the file names should be LD_1234_waypoint_navigation.bag and LD_1234_waypoint_navigation.py.


zip -r LD_<team_id>.zip LD_<team_id>_waypoint_navigation.bag LD_<team_id>_waypoint_navigation.py
This should be the structure of zip file
|__LD_1234.zip
… |__LD_1234_waypoint_navigation.bag
… |__LD_1234_waypoint_navigation.py

- Step 5: Submit this zip file on the portal in the place of Task 2A and check your score.


## Task 2B Locating and Identifying Organisms in Their Habitat
Aim:
The aim of this task is to fly the Swift drone over the surface of the exoplanet and identify the organism present in the simulation environment in Gazebo.
Prerequisites
It is presumed that you have successfully completed Task 1B as well as Task 2A. You should also go through the ROS-OpenCV resources provided in Task2 before attempting this task. Finally we encourage you to go the resources on the internet!
Installations
We’ve pushed new code to the exisiting package. You simply need to pull it and run catkin build

```
cd ~/catkin_ws/src/luminosity_drone

git pull origin ros_pkg --recurse-submodules

cd ~/catkin_ws

catkin build

cd ~/catkin_ws/src/luminosity_drone/luminosity_drone/src

sudo chmod +x info spawning colony
```

#### Problem Statement
In this task you will use computer vision techniques to find the location (whycon coordinates) of the image taken from the drone where the organism is detected.

The organisms are simulated using LEDs in the gazebo simulation environment.

You have to identify the location (whycon coordinate) of the organism on the surface of the exoplanet(arena).

Publish the location and the type of organisms onto a ROS topic.

Go to the research station and land the swift drone.

Procedure
Launch the Gazebo simulation world containing the arena of the exoplanet by typing the following command

```
roslaunch luminosity_drone task_2b.launch
```

Make a new python script life_form_detector.py in the lcatkin_ws/src/luminosity_drone/luminosity_drone/scripts folder and complete the script to fly the drone through the arena and detect the organisms.

Make a search algorithm by giving a path to the Swift drone.

Throughout the entire flight, deploy image processing with the onboard camera on the Swift drone in an effort to identify organisms.

As soon as you detect the organism in the camera frame, try to align th centroid of the LED to the center of the camera frame.

The different organism type according to the no. of LEDs are given below:

No. of LEDs	Organism Type
```
2	alien_a
3	alien_b
4	alien_c
```
Once you are confident about the alingment, you have to publish the type of organisms and the Whycon coordinates onto the the following ROS topic astrobiolocation having message type Biolocation

Biolocation Message type:


```
  arun@eyantra:~/catkin_ws$ rosmsg show luminosity_drone/Biolocation
  string organism_type
  float64 whycon_x 
  float64 whycon_y 
  float64 whycon_z
```
  
Finally, go to the position [11, 11, 37], disarm and land the drone at the research station.

📌 Note

The organism will spawn at some random location every time you launch the task.
Each time an organism is located, publish onto the ROS topic called astrobiolocation only once.
The time taken to identify the organism is not taken as a parameter for scoring.
The total evaluation time is 120 secs, so be careful to complete the task within that time frame.
#### Recording and Submission instructions
- Step 1: Tune your python script to fly the drone, identify the organism and fly to the research station.

- Step 2: Now you need to record your submission, a tool named rosbag helps to record rostopics just as a video. When you feel confident with the performance of your PID controller and you are ready to record the submission, use another launch file which will run the same things as in task_1.launch as well as start the life_form_detector and a node to record rosbag after 5 seconds delay so that gazebo starts and drone is spawned. Use this launch file to implement the task and record a bag file for 2 minute i.e. 120 seconds
```
roslaunch luminosity_drone task_2b_submission.launch
```
- Step 3: This will generate a bag file named life_form_detector_<date_time>.bag in the scripts folder, change the name to LD_<team_id>_life_form_detector.bag, you need to make a zip file containing this bag file and the python script, change the name of python script to LD_<team_id>_life_form_detector.py.
NOTE: The zip should contain only 2 files in the root directory, DO NOT make a folder and then zip, directly zip the two files. You can use this command to zip the file. Use this command only after you have renamed both the files. replace <team_id> with your team id, for eg. if your team id is 1234, then the file names should be LD_1234_life_form_detector.bag and LD_1234_life_form_detector.py.

```
zip -r LD_<team_id>.zip LD_<team_id>_life_form_detector.bag LD_<team_id>_life_form_detector.py
```
This should be the structure of zip file
|__LD_1234.zip
… |__LD_1234_life_form_detector.bag
… |__LD_1234_life_form_detector.py

- Step 4: Submit this zip file on the portal in the place of Task 2B and check your score.
YouTube Video
Record the video using a screen recorder like kazam or simplescreen recorder. You can install them using the following commands:

```
sudo apt install kazam
```
```
sudo apt install simplescreenrecorder
```
Start recording the video, At the start terminal should be visble where you will launch a file and node.

Once you start your script your screen should have both gazebo and camera output as shown in the following image for most of the time:


`Upload a one-shot continuous video with the title LD_<team_id>_Task2B (For example: If your team ID is 1234 then, save it as LD_1234_Task2B)`

Please note that while uploading the video on YouTube select the privacy setting option as Unlisted




## Task 2C (bonus) Exoplanetary Surface Organism Detection and Identification
Aim:
The aim of this task is to fly the Swift drone over the surface of the exoplanet and identify the organisms present at different set points in the simulation environment in Gazebo.
Prerequisites
It is presumed that you have successfully completed Task 2B. Task 2C is a bonus task. It is not mandatory to complete the task but those who are interested can finish the task and it will be evaluated.
Problem Statement
In this task you will use computer vision techniques to find the location (whycon coordinates) of the image taken from the drone where the organism is detected.

The organisms are simulated using LEDs in the gazebo simulation environment.

You have to identify the location (whycon coordinates) of the organisms on the surface of the exoplanet(arena).

Publish the location and the type of organisms onto a ROS topic.

Go to the research station and land the swift drone.

Procedure
Launch the Gazebo simulation world containing the arena of the exoplanet by typing the following command

```
roslaunch luminosity_drone task_2c.launch
```
Make a new python script biota_detector.py in the lcatkin_ws/src/luminosity_drone/luminosity_drone/scripts folder and complete the script to fly the drone through the arena and detect the organisms.

Make a search algorithm by giving a path to the Swift drone.

Throughout the entire flight, deploy image processing with the onboard camera on the Swift drone in an effort to identify organisms.

As soon as you detect the organism in the camera frame, try to align th centroid of the LED to the center of the camera frame.

The different organism type according to the no. of LEDs are given below:

No. of LEDs	Organism Type
```
2	alien_a
3	alien_b
4	alien_c
```
Once you are confident about the alingment, you have to publish the type of organisms and the Whycon coordinates onto the the following ROS topic astrobiolocation having message type Biolocation

Biolocation Message type:

```

  arun@eyantra:~/catkin_ws$ rosmsg show luminosity_drone/Biolocation
  string organism_type
  float64 whycon_x 
  float64 whycon_y 
  float64 whycon_z
```
  
You have to repeat this procedure for every organism present on the exoplanet surface.

Finally, go to the position [11, 11, 37], disarm and land the drone at the research station.

📌 Note

The organism will spawn at some random location every time you launch the task.
Each time an organism is located, publish onto the ROS topic called astrobiolocation only once.
The time taken to identify the organism is not taken as a parameter for scoring.
The total evaluation time is 180 secs, so be careful to complete the task within that time frame.
#### Recording and Submission instructions
- Step 1: Tune your python script to fly the drone, identify the organism and fly to the research station.

- Step 2: Now you need to record your submission, a tool named rosbag helps to record rostopics just as a video. When you feel confident with the performance of your PID controller and you are ready to record the submission, use another launch file which will run the same things as in task_1.launch as well as start the biota_detector and a node to record rosbag after 5 seconds delay so that gazebo starts and drone is spawned. Use this launch file to implement the task and record a bag file for 3 minute i.e. 180 seconds
```
roslaunch luminosity_drone task_2c_submission.launch
```
- Step 3: This will generate a bag file named biota_detector_<date_time>.bag in the scripts folder, change the name to LD_<team_id>_biota_detector.bag, you need to make a zip file containing this bag file and the python script, change the name of python script to LD_<team_id>_biota_detector.py.
NOTE: The zip should contain only 2 files in the root directory, DO NOT make a folder and then zip, directly zip the two files. You can use this command to zip the file. Use this command only after you have renamed both the files. replace <team_id> with your team id, for eg. if your team id is 1234, then the file names should be LD_1234_biota_detector.bag and LD_1234_biota_detector.py.

```
zip -r LD_<team_id>.zip LD_<team_id>_biota_detector.bag LD_<team_id>_biota_detector.py
```
This should be the structure of zip file
|__LD_1234.zip
… |__LD_1234_biota_detector.bag
… |__LD_1234_biota_detector.py

- Step 4: Submit this zip file on the portal in the place of Task 2C and check your score.
YouTube Video
Record the video using a screen recorder like kazam or simplescreen recorder. You can install them using the following commands:

```
sudo apt install kazam

sudo apt install simplescreenrecorder
```
Start recording the video, At the start terminal should be visble where you will launch a file and node.

Once you start your script your screen should have both gazebo and camera output as shown in the following image for most of the time:


Upload a one-shot continuous video with the title LD_<team_id>_Task2C (For example: If your team ID is 1234 then, save it as LD_1234_Task2C)




