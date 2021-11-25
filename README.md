# MirrorLabs_HL2

This repository is a modificatiion of Unity project made be Doris Ashenbenner and Jonas Rieder from TU Delft as a part of MirrorLabs. You can find the original project [here](https://data.4tu.nl/articles/software/Framework_for_the_publication_MirrorLabs_creating_similar_learning_environments_for_students_all_over_Europe_for_human-robot_coproduction/14186807).

## Prerequisites

- ROS machine with ROS Noetic or Melodic.
- Unity side of things should be done on Windows machine
- [Unity Hub](https://unity3d.com/get-unity/download)
- [Unable Developer Mode on Hololens and Windows Machine](https://docs.microsoft.com/en-us/windows/mixed-reality/develop/advanced-concepts/using-visual-studio?tabs=hl2)

## Installation

### Hololens side

1. Clone this repository.
2. Open Unity Hub.
    - If this is your first time using Unity Hub, license should be activated:
        1. Go to settings (gear in the corner)
        2. Go to manage license tab.
        3. Log into Unity account or create one, when asked.
        4. Press activate new license button.
        5. Choose personal and choose the answer, which suits you after that.
        6. Personal license will be acctivated.
3. Press ADD button and choose the [MirrorLabs_HL2](https://github.com/ut-ims-robotics/MirrorLabs_HL2/tree/main/MirrorLabs_HL2) folder (not the repository folder, but nested one)
4. Install the unity version, which you will be asked.
    - During the installation make sure to check Visual Studio 2019, if you don't have it installed
    - And make sure to check Universal Windows Platform (UWP) Support and Windows build support. If you miss this step, you can add them later in the installs tab if you press 3 dots on the Unity version and choose Add Modules option
5. After installation open the project. Skip the prompt about new unity version.
6. In the prooject panel navigate to Assets/MirrorLabs/Scenes and double click on ML_UniversalRobotics_ur5_modified scene. This will open the scene in unity.
7. In the Hierarchy window unfold RosConnectors game object
8. Click on one of two object and in Ros Connector (Script) change Ros Bridge Server Url and Ros Bridge Server_IP with the IP of your ROS machine. Port for Url should remain the same.
9. Do the same with the remaining object.
10. Go to File -> Build Settings.
11. Make sure, that UWP is chosen (if not, choose it and press switch platform)
12. Verify that only the currrent scene is chosen in the Scenes in Build window.
13. Set target device to Hololens and Architecture to ARM64.
14. Press build and choose folder where to save the built project.
15. After building go to the specified folder and open the solution file.
16. Go to Project -> Properties and to Debugging tab.
17. Fill in Machine Name with the ip Hololens 2
18. Under the menu bar change debug to release, ARM to ARM64 and set to remote machine and press start debugging.
19. After deploying to Hololens, app will launch automatically, but you will be able to open it yourself from the app menu on the hololens

### ROS side

1. Make sure moveit and moveit_visual_tools are installed.
2. Install rosbridge_suite.
3. Clone [Universal Robot repository](https://github.com/ros-industrial/universal_robot) into src folder of your catkin workspace.
    - Depending on your controller box and software, you might also need the [following repository](https://github.com/UniversalRobots/Universal_Robots_ROS_Driver).
4. Clone the [following package](https://github.com/ut-ims-robotics/hl_ur5_ik) into src folder of your catkin workspace.
5. Build Everything

## Running the setup

### ROS side

1. Source your workspace
2. Launch the robot with moveit
    - For simulated one run `roslaunch ur5_moveit_config demo.launch`
    - For real robot follow the quick start instructions from either [this](https://github.com/ros-industrial/universal_robot) or [this](https://github.com/UniversalRobots/Universal_Robots_ROS_Driver) repositiories. It depends on the controller box and software.
3. Launch rosbridge with command `roslaunch rosbridge_server rosbridge_websoocket.launch`
4. Start the communication node with `rosrun hl_ur5_ik ur_ik_request`

### Unity side

1. Make sure to be in the same network as ROS machine.
2. Start the ML_M1013 app
3. If the setup is done correctly,  Hololens will connect to the ROS machine and you will be able to set the TCP goal in the form of a sphere, while previewing the robot. To send the goal, release the sphere.
