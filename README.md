# Control-of-two-UR5s-by-two-phantom-omnies-

# University of Manchester - Sungho Woo, Vivi pazos.

#This project was designed during the summer internship of the University of Manchester in 2019. This user manual was simply described for the beginner of ROS.  Some problems can occur when you do catkin_make if you do not download some necessary dependencies. So you are required to do some trouble shooting but everything is on GOOGLE. 

*Environment:
-Ubuntu 16.04
-ROS Kinetic 
-UR5 
-Two LAN mode phantom Omnis ( 2016.1-1 driver) 
-Two laptops (ROS Network)

#Demonstration vedio :  https://youtu.be/ZUHPw8gEjiA

Before you launch the files you should make sure that every folder work well by cakin_make

#Auto necessary dependency installation:
rosdep update
rosdep install --rosdistro kinetic --ignore-src --from-paths src

#Launch Process 
-- Connection of Geomagic phantom haptic
1. install the haptic driver in geomagic_touch_device_driver_2016.1-1-amd64 
2. launch Geomagic_Touch_Setup
3. Check the connection by Geomagic_Touch_Diagnostic
4. Type: roslaunch geomagic_control geomagic.launch  (If it works well, the robot  looks blue and mimics the motion of your phantom haptic. If you want to use the twin arms not a single arm, you should launch geomagic_control geomagic_headless.launch)
-- the UR
5. Type: roslaunch summer_gazebo summer_twin.launch (you can also find summer_ robot.launch for the single robot operation.)
6. Type: rosrun summer_gazebo send_summer2.py ( this makes that each of  UR5 joint reads each value of phantom omni joint.  you should check the corresponding of the topics between the UR5 and phantom omni. For the single-arm: send_summer.py)
7. Force feed back :  rosrun geomagic_control lockDoF2.py (For the single-arm: lockDof.py)

#To use both UR5 arms you should use the ROS connection which uses a master computer and slavery computer.  you need to correspond both computer network IP by using [gedit .bashrc]. This part needs little knowledge of ROS.  Change the topic of the slavery phantom omni from [geomagic1] to [geomagic] in omni.cpp . Then type:  rosrun summer_gazebo send_summer1.py on the slavery computer to avoid the interruption of the topics. Force feedback is also applied to launch on the slavery computer like the same process above( check the topic).

