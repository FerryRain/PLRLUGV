# graduation_design_PLTD3


## 算法当前存在问题
#### 当前模型测试问题
1. 机器人在初始化后，若遇到障碍物较为紧密（例如前方很近的地方都是障碍物或只有可通行空间极小），机器人会由于训练时的奖励函数惩罚机器人后退，而不太敢后退以寻求更优路径


#### 训练策略
1. 单训练 27h未收敛
2. 无障碍物 -> 有障碍物 -> 动态障碍物 26h收敛
3. 奖励值修改 增加单步惩罚（当前幕开始距离 / 决策步数） 增加角速度惩罚 -> 鼓励向目标接近 18h收敛

## Build the Project
#### Build ROS Code
```shell
cd {Your PROJECT PATH}/catkin_ws
catkin_make_isolated
```

#### SET bashrc to update the ros environment:
```shell
export ROS_HOSTNAME=localhost
export ROS_MASTER_URI=http://localhost:11311
export ROS_PORT_SIM=11311
export GAZEBO_RESOURCE_PATH=~/DRL-robot-navigation/catkin_ws/src/multi_robot_scenario/launch
source {Your PROJECT PATH}/devel_isolated/setup.bash
```

#### And then reload the file bashrc
```shell
source ~/.bashrc
```
#### Install The Python Package or Creat the new environment of conda
```shell
# INSTALL THE PYTHON PACKAGE
pip install -f requirements.txt
```
or
```shell
# CREATE THE NEW conda ENVIRONMENT
conda env create -f environment.yml
```

#### Train the model
```shell
cd {Your PROJECT PATH}/TD3
python3 train_velodyne_td3.py
```

#### To kill the training process:
```shell
killall -9 rosout roslaunch rosmaster gzserver nodelet robot_state_publisher gzclient python python3
```


#### Once training is completed, test the model:
```shell
cd {Your PROJECT PATH}/TD3
python3 test_velodyne_td3.py
```