# rdk-x3

### リンク

- https://d-robotics.github.io/rdk_doc/en/RDK
- https://archive.d-robotics.cc/

GitHub
- https://github.com/D-Robotics/hobot_mipi_cam

### MIPI Cameraをプレビューする

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

