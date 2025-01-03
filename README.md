# RDK X3

### リンク
- https://d-robotics.github.io/rdk_doc/en/RDK
- https://archive.d-robotics.cc/

GitHub
- https://github.com/D-Robotics/hobot_mipi_cam
- https://github.com/D-Robotics/rdk_model_zoo
- https://github.com/D-Robotics/line_follower

RealSense
- https://github.com/IntelRealSense/librealsense
- https://github.com/IntelRealSense/realsense-ros/tree/ros2-development

### MIPI CameraをWebブラウザプレビューする

**Console1** (Aquired raw image from mipi camera)
```bash
$ . /opt/tros/humble/setup.bash
$ ros2 launch mipi_cam mipi_cam.launch.py mipi_video_device:=IMX219
```
**Console2** (Encode to jpeg image)
```bash
$ . /opt/tros/humble/setup.bash
$ ros2 launch hobot_codec hobot_codec_encode.launch.py
```
**Console3** (Publich to websocket)
```bash
$ . /opt/tros/humble/setup.bash
$ ros2 launch websocket websocket.launch.py websocket_image_topic:=/image_jpeg websocket_only_show_image:=true
```
**Open a web browser** and enter `http://IPAddress:8000`

### MIPI CameraをRVIZでプレビューする

**※ WSLの場合はWindowのファイアウォールを解放する必要がある**  
https://qiita.com/zakutakumi/items/fb1be336b06d73bbd1cb

On the device
```
$ ros2 launch mipi_cam mipi_cam.launch.py mipi_out_format:=bgr8 mipi_image_width:=480 mipi_image_height:=272 mipi_io_method:=ros mipi_video_device:=IMX219
```

On the devlopment pc
```
$ ros2 run rviz2 rviz2
-> Add
    -> By topic
        -> /image_raw
            -> image
```

### MIPI CameraをRQtでプレビューする

On the device
```
$ ros2 launch mipi_cam mipi_cam.launch.py mipi_video_device:=IMX219

$ ros2 launch hobot_codec hobot_codec_encode.launch.py codec_out_format:=jpeg codec_pub_topic:=/image_raw/compressed
```

On the development pc
```
$ sudo apt-get install ros-humble-rqt-image-view ros-humble-rqt ros-humble-image-transport-plugins

$ ros2 run rqt_image_view rqt_image_view
-> Select /image_raw_compressed
```

### RealSenseをプレビューする

On the device
```
$ sudo apt-get install ros-$ROS_DISTRO-librealsense2*
$ sudo apt-get install ros-$ROS_DISTRO-realsense2-*

$ ros2 launch realsense2_camera rs_launch.py enable_infra1:=true pointcloud.enable:=true
```

On the development pc
```
$ ros2 run rviz2 rviz2
```
