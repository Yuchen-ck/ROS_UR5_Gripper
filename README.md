# UR5 and MoveIt! (ROS Noetic)

本專案使用 **ROS Noetic** 來控制 **UR5 + Robotiq Gripper**，並透過 **MoveIt!** 進行運動規劃與 Gazebo 模擬。

---

## **📌 1. 安裝 ROS Noetic**

如果你的系統還沒有安裝 ROS Noetic，可以使用以下指令：

```sh
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros-latest.list'
curl -sSL 'https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc' | sudo apt-key add -
sudo apt update
sudo apt install -y ros-noetic-desktop-full
```

🔹 **初始化 ROS 環境變量**

```sh
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

🔹 **安裝 ROS 工具**

```sh
sudo apt install -y python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
sudo rosdep init
rosdep update
```

---

## **📌 2. 安裝 MoveIt!**

```sh
sudo apt install -y ros-noetic-moveit
```

🔹 安裝 **MoveIt! 相關套件**：

```sh
sudo apt install -y ros-noetic-moveit-ros-planning ros-noetic-moveit-ros-move-group ros-noetic-moveit-kinematics
```

---

## **📌 3. 建立 ROS 工作區 (Workspace)**

```sh
mkdir -p ~/ur_ws/src
cd ~/ur_ws
catkin_make
source devel/setup.bash
```

🔹 **確保 ROS 工作區正確被讀取**：

```sh
echo "source ~/ur_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---

## **📌 4. 下載 UR5 MoveIt! 配置檔**

🔹 安裝 **Universal Robots 套件**：

```sh
cd ~/ur_ws/src
git clone -b noetic-devel https://github.com/ros-industrial/universal_robot.git
cd ~/ur_ws
rosdep install --from-paths src --ignore-src -r -y
catkin_make
source devel/setup.bash
```

---

## **📌 5. 執行 MoveIt! UR5 模擬環境**

🔹 **執行 MoveIt! 主要啟動檔 in Rviz**：

```sh
roslaunch ur5_moveit_config demo.launch
```
🔹 **啟動node 控制手臂**：

```sh
rosrun ur_test test_node
```
## test_node: Rviz有顯示手臂跑隨機路徑，代表測試成功。

📌 Open Rviz and Gazebo 還有Bug需解決
