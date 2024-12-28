# RDK X3

### リンク
- https://d-robotics.github.io/rdk_doc/en/RDK
- https://archive.d-robotics.cc/

GitHub
- https://github.com/D-Robotics/hobot_mipi_cam
- https://github.com/D-Robotics/rdk_model_zoo
- https://github.com/D-Robotics/line_follower

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
