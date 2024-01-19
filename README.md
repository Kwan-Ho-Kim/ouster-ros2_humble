# ouster-ros2_humble

## Requirements
```
rosdep install --from-paths $OUSTER_ROS_PATH -y --ignore-src
```

### Linux

```bash
sudo apt install -y             \
    ros-$ROS_DISTRO-pcl-ros     \
    ros-$ROS_DISTRO-tf2-eigen   \
    ros-$ROS_DISTRO-rviz2
```
```
sudo apt install -y         \
    build-essential         \
    libeigen3-dev           \
    libjsoncpp-dev          \
    libspdlog-dev           \
    libcurl4-openssl-dev    \
    cmake                   \
    python3-colcon-common-extensions
```

## Getting Started

```bash
mkdir -p ros2_ws/src && cd ros2_ws/src
git clone -b ros2 --recurse-submodules https://github.com/ouster-lidar/ouster-ros.git
```

```bash
source /opt/ros/<ros-distro>/setup.bash # replace ros-distro with 'rolling', 'humble', or 'iron'
```

```bash
cd ros2_ws
colcon build --symlink-install --cmake-args -DCMAKE_BUILD_TYPE=Release
```

```bash
source ros2_ws/install/setup.bash
```

#### Sensor Mode
```bash
ros2 launch ouster_ros sensor.launch.xml    \
    sensor_hostname:=<sensor host name>
```
The equivalent python launch file is:
```bash
ros2 launch ouster_ros driver.launch.py    \
    params_file:=<path to params yaml file>
```

#### Recording Mode
```bash
ros2 launch ouster_ros record.launch.xml    \
    sensor_hostname:=<sensor host name>     \
    bag_file:=<optional bag file name>      \
    metadata:=<json file name>              # optional
```

#### Replay Mode

```bash
ros2 launch ouster_ros replay.launch.xml    \
    bag_file:=<path to rosbag file>         \
    metadata:=<json file name>              # optional if bag file has /metadata topic
```

#### Multicast Mode (experimental)
```bash
roslaunch ouster_ros sensor_mtp.launch.xml  \
    sensor_hostname:=<sensor host name>     \
    udp_dest:=<multicast group ip (ipv4)>   \
    mtp_main:=true                          \
    mtp_dest:=<client ip to receive data>   # mtp_dest is optional
```

```bash
roslaunch ouster_ros sensor_mtp.launch.xml  \
    sensor_hostname:=<sensor host name>     \
    udp_dest:=<multicast group ip (ipv4)>   \
    mtp_main:=false                         \
    mtp_dest:=<client ip to receive data>   # mtp_dest is optional
```

#### GetMetadata
```bash
ros2 service call /ouster/get_metadata ouster_srvs/srv/GetMetadata
```

#### GetConfig
```bash
ros2 service call /ouster/get_config ouster_srvs/srv/GetConfig
```

#### SetConfig
```bash
ros2 service call /ouster/set_config ouster_srvs/srv/SetConfig \
    "{config_file: 'some_config.json'}"
```

#### Reset
```bash
ros2 service call /ouster/reset std_srvs/srv/Empty
```


from https://github.com/ouster-lidar/ouster-ros.git
