## Point grey cameras
```
roslaunch pointgrey_camera_driver camera.launch camera_serial:=xxxxxxx1
roslaunch pointgrey_camera_driver camera.launch camera_serial:=xxxxxxx2

rosrun image_view image_view image:=/camera/image_color
```

## Install Velodyne packages

```
git clone https://github.com/ros-drivers/velodyne.git

# now copy folders so that it is like following

~/catkin_ws$ ls src
CMakeLists.txt  velodyne_driver     velodyne_msgs
velodyne        velodyne_laserscan  velodyne_pointcloud
```
### Install dependencies

```

~/catkin_ws$ rosdep install --from-paths src --ignore-src -r -y
~/catkin_ws$ catkin_make

```


## Launch velodyne ROS node

```
$ roslaunch velodyne_pointcloud VLP16_points.launch

# It should show the velodyne nodes now
$ rosnode list

/velodyne_nodelet_manager
/velodyne_nodelet_manager_cloud
/velodyne_nodelet_manager_driver
/velodyne_nodelet_manager_laserscan

# Verify we get echo - should output in console continuously
$rostopic echo /velodyne_points


# Visualize

$ rosrun rviz rviz -f velodyne
```

From Displays add PointCloud2 output type and select ```/velodyne_points``` as topic

![RViz VLP-16][rvizvlp16]

[rvizvlp16]: images/rviz_vlp16.png "RViz VLP-16"
