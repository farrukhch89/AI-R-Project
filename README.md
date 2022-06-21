# AI-R-Project
Artificial Intelligence and Robotics
BSCH-AIR – Project

Course 	 BSCH-AIR
Stage / Year 	4
Module 	AI & Robotics 
Semester 	2
Assignment 	Group Project 
Date of Title Issue 	6th April 
Assignment Deadline 	8th May, 23:55pm
Assignment Submission 	Upload to Moodle 
Assignment Weighting 	60% of module 

Group Project 
You will be working in groups of three to complete this project.  Respond on Moodle with the names and student numbers of the people in your group. An official group list will be posted on Moodle, here you will receive your official Group Name. I suggest that you work through Google Drive with this document being stored as a Google Doc so that all teammates can work on it together. I recommend that you use Git in order to work collaboratively. There are instructions on Moodle on how to integrate the environment with Git. 
Submission
-	Items to submit 
o	Folder called ‘GroupName’ containing 3 packages
o	This bottom of this document after the ----- line  
-	To ensure that all submissions are identical please do the following
o	Partner 1 should create a zip file of all materials and email it to all teammates
o	Partner 1 should upload the zip file 
o	The other teammates should unzip the file and once satisfied that it is correct upload the ORIGINAL zip file unedited
o	I will be doing md5 hashing to ensure that all team members’ submissions are 100% bitwise identical.
-	All code must be clearly commented
-	All work should be original

Workspace
We will be using the workspace AIR Group Project Rosject. You will be creating your own Rosject forked from this Rosject: https://app.theconstructsim.com/#/l/49d76051/
Please report any difficulties you have with this workspace on Moodle so that I can resolve them quickly.

Tasks
Included in Robot Ignite is a notebook with tasks and tips on how to complete them. You will be awarded marks for performing the tasks specified below. 

Hints 
-	Useful overview https://github.com/cse481sp17/cse481c/wiki/Lab-16:-Mapping-and-navigation
-	Standard Units in ROS https://www.ros.org/reps/rep-0103.html
-	move_base API http://wiki.ros.org/move_base
-	Remember to complete ROS Navigation in 5 Days (Similar tasks)

Troubleshooting
-	Logout for 10 mins if you are experiencing: 
-	rviz running multiple times 
-	Unknown processes running in the background
-	If a map/laser/particlecloud/plan is not visible 
o	Make sure the appropriate node is running 
o	Make sure that the element is subscribed to the correct topic in rviz
-	If you get the following error, then you will need to publish a transform from the base_link to the map. I would recommend all zeros. Call this file project_planning_transform_base_link_to_map.launch
o	WARN] [1555404987.356642374, 848.696000000]: Timed out waiting for transform from base_link to map to become available before running costmap, tf error: canTransform: target_frame map does not exist.. canTransform returned after 0.1 timeout was 0.1.
-	If you get the following error you will need to set up the maps correctly as you are not using the correct map
o	[ERROR] [1555406187.405033105, 1261.958000000]: None of the points of the global plan were in the local costmap, global plan points too far from robot

Package Creation
Create 3 new packages all with rospy as a dependency
1.	project_mapping
2.	project_localization
3.	project_planning













1. project_mapping – 50 marks
Your final file tree should be similar to:
user:~/catkin_ws/src$ tree ./project_mapping
./project_mapping
├── CMakeLists.txt
├── launch
│   ├── project_mapping.launch
│   └── project_mapping_transforms.launch
├── map
│   └── project_mapping.bag
│   └── project_mapping_map.pgm
│   └── project_mapping_map.yaml
├── package.xml
├── param
│   └── project_mapping_params.yaml
├── project_mapping_explanation.txt
├── rviz
│   └── project_mapping_rviz.rviz
├── src
└── tf
    ├── frames.gv
    ├── frames.pdf
    └── tf_monitor.txt

1.	10% - Create a launch file which adds a nerf_cannon to the robot.
o	Launch file name: project_mapping_transforms.launch
o	Launch file contents: The file should enable the following 
	The addition of a nerf_cannon to the base_link 
	Positioned 10cm higher than the base_link
	It should shoot at 45 degrees above horizontal 
	It’s transform should be sent at 10Hz
	Comment the file
	The nerf_cannon will not appear as an object but will appear in the transform tree
o	Hints: 
	Ex. 2.10

2.	5% - Create a pdf file frames.pdf to show that this transform has been correctly added
o	Documentation: 
	Include a screen shot and appropriate comment 
	Include screen shot of command used
o	Hints: Ex 2.9

3.	5% - Create a txt file called tf_monitor.txt which contains a list of the transforms between odom and the nerf_cannon.  
o	Hints: 
	tf_monitor in http://wiki.ros.org/tf/Debugging%20tools
	you can copy and pasete or redirect the output to file using https://www.tutorialspoint.com/unix/unix-io-redirections.htm

4.	5% - Create a Rviz config file showing various elements related to mapping. You may need to update this as you progress with the section.
o	Rviz config file name: project_mapping_rviz.rviz
o	Rviz config file contents: Save the correct configuration of the following elements linked to appropriate topics where possible:  
	GlobalOptions
	Grid
	Map
	RobotModel
	TF
	LaserScan
o	Documentation 
	Include a screen shot and an appropriate comment 
o	Hints: 
	Ex 2.1

5.	10% - Create a launch file and a param file for the slam_gmapping node 
o	Launch file name: project_mapping.launch
o	Param file name: project_mapping_params.yaml
	contents: edit 5 of the default parameters
o	Documentation: 
	Explain the effect of the editing of the 5 default parameters in the yaml file
o	Hints: 
	Ex 2.11 to 2.15

6.	5% - Launch the node using the launch file that you’ve just created and create a map of the environment. 
7.	5% - Save the map that you’ve just created. 
o	Map files names: 
	project_mapping_map.pgm
	project_mapping_map.yaml
o	Hints: 
	Ex 2.17 to 2.18
	Make sure all relevant topics are being published (show screen shot)
o	Documentation: 
	Explain the parameters which appear in project_mapping_map.yaml 
	Include a screen shot of the pgm file

8.	5% - Create a launch file that launches the map_server node
o	Launch file name: map_provider.launch
o	Documentation:
	Explain the parameters used in map_provider.launch

2. project_localization – 25 marks

Your final file tree should look similar to: 
user:~/catkin_ws/src$ tree ./project_localization/
./project_localization/

├── CMakeLists.txt
├── launch
│   ├── project_localization.launch
│   └── project_localization_move.launch
├── package.xml
├── param
│   └── project_localization_params.yaml
├── rviz
│   └── project_localization_rviz.rviz
└── src
    └── project_localization_move.py

1.	5% - Save a copy of the rviz configuration that you use in project_localization_rviz.rviz It should have the following items
o	PoseArray 
o	any other appropriate items
o	Documentation
	Include a screen shot and appropriate comment 

2.	20% - Create the project_localization package which provides the following functions 
o	Initiate all necessary processes through a single launch file this may call other launch files
o	Initiate dispersal of all particles randomly throughout the free space 
o	Gather these particles as the robot has localized itself on the map using a repetitive movement process 
o	Hints: 
	Ex 3.1 to 3.12 
	Start with the robot in a room for faster localization
o	Documentation:
o	Provide a screen capture of 
	the dispersed particle cloud 
	it progressively getting smaller
	it localized to the robot.
o	Comment on the outcome, which may or may not be successful







3. project_planning – 25 marks
Your final file tree should be similar to:
CMakeLists.txt  config  launch  package.xml  rviz  src
user:~/catkin_ws/src/project_planning$ tree
├── CMakeLists.txt
├── config
│   ├── costmap_common.yaml
│   ├── costmap_global.yaml
│   ├── costmap_local.yaml
│   ├── global_planner.yaml
│   ├── localization.yaml
│   ├── local_planner.yaml
│   ├── mapping.yaml
│   └── move_base_params.yaml
├── launch
│   ├── project_planning_send_goal.launch
│   └── project_planning_transform_base_link_to_map.launch // only construct if necessary 
├── package.xml
├── rviz
│   └── project_planning_rviz.rviz
└── src
      └── project_planning_send_goal.py

1.	5% - Save a copy of the rviz configuration that you use in project_planning_rviz.rviz It should have the following items
o	a map for both local and global costmaps (choose difference colour schemes for each).
o	a path for both local and global plans (choose different colours for each)
o	PoseArray 
o	any other appropriate items
o	Documentation
	Include a screen shot and appropriate comment 
2.	5% - Create a launch file that will launch the move_base node, and the necessary parameter files in order to properly configure the move_base node.
o	    Naming: 
	project_move_base.launch
	project_move_base_params.yaml
o	Documentation 
	Provide supporting screen shots and high-level explanation 
3.	5% -  Create the necessary parameter files in order to properly configure the global and local costmaps.
4.	5% - Create the necessary parameter files in order to properly configure the global and local planners.
5.	5% - Launch the node and check that everything works fine.
o	Launch file name: project_planning_send_goal.launch
o	This file should also launch other necessary processes to facilitate the planning process
	You may want to base this file on move_base_demo.launch and send_goal.launch from the examples 
o	Documentation 
	Provide supporting screen shots and high-level explanation
4. Additional Task for Groups of 3 - Add additional items to the environment – 33 marks

•	Use UDRF files to define 5 geometrical objects. 
•	Use the following file as an example /home/user/catkin_ws/src/object.urdf 
•	Place these objects in the environment. 
•	Clearly document the commands used to place these objects.
•	Describe the attributes of these objects and how this affects the way the robot interacts with them.
•	Document these objects.
•	Hint: 
o	Ex 1.4


Project Demonstration
During the final lab session, you will be split into breakout rooms according to your Project Group. Each group will be given 10 minutes to demonstrate their project collectively. For the demonstration, 1 group member will run the Construct rosject on their machine and share their screen. 

You may be asked to show:
-	The robot in movement
-	Generation of a map
-	Loading a map
-	Robot Localisation
-	Rviz visualisation
-	Code (Launch and py files) and explain their content
-	Robot Planning
-	Incorporation of objects in the environment
-	Any additional features
-	Division of Labour/works carried out
-	Etc
 
--------------------------------------------------- delete above this line-----------------------------------

Name 1: 					 Student Number: ¬			
Name 2: 					 Student Number: ¬			
Name 3: 					 Student Number: ¬			

Documentation & Screen Shots
Provide screen shots indicating the completion of each section where appropriate and a description below of what they show. 
Evaluate the results achieved and comment on the factors which affected these outcomes.

1.	project_mapping(documentation & screenshots)

2.	project_localization (documentation & screenshots)

3.	project_planning (documentation & screenshots)

4.	additional features (documentation & screenshots) 

5.	Additional Task for Group of 3 - Add additional items to the environment (documentation & screenshots) 

Division of Labour
Please complete the sections below with regard to the estimate of the division of work between the group partners
Summary of division of work
If the work was split in the range of 45% to 55% per partner then that is fine and simply say “Work was evenly divided”. If this was not the case then state with a summary sentence. This is the important statement of this file.

Division of work : work was evenly divided 
Filename / Task	Student Name 1	Student Name 2	Student Name 3 
project_mapping			
project_localization			
project_planning			
Other items	40%	10%	50%
….			

Percentage of work completed by each partner on each class / task 
Some area requires more work than others so this is only for reference. An average of these values will not be calculated.

Please ensure that all students contribute to the research. The remaining topics can be divided among the students, but each student must apply at least 1 techniques. 
![image](https://user-images.githubusercontent.com/47636486/174781065-e966b5a0-3aff-4e5b-b441-12260a4105c2.png)
