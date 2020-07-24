# USB CAM ROS2 Node

> DGIST ARTIV Lab.
> Autonomous Vehicle Research Group

Original code from ros2_usb_camera@https://github.com/klintan/ros2_usb_camera

#### this fork version has distinct feature from original version
- USB CAM node for ros2 works with UVC camera (Logitech...)
- Support __4K BRIO Camera__ or work with __over 60fps camera__


Features
- Compressing image
- MJPG Format based usb cam ros publisher

### Topics
- `/camera_info` - topic for camera info
- `/image_raw` - topic for raw image data

## Installation

Need to build with ROS2 Build system : Colcon
`colcon build`

## Usage

`ros2 run usb_camera_driver usb_camera_driver_node`

Available parameters:
- `frame_id` -> transform frame_id of the camera, defaults to "camera"
- `image_width` -> image width (1280 default)
- `image_height` -> image height (720 default)
- `fps` -> video fps (60 default)
- `camera_id` -> id of camera to capture (0 - 100, 0 default)

### Calibration files
To use the camera info functionality you need to load a file from the camera_calibration (https://github.com/ros-perception/image_pipeline/tree/ros2/camera_calibration) library and put it in/name it `file:///Users/<youruser>/.ros/camera_info/camera.yaml`


### Compressed images

To get compressed images (works seamlessly with web streaming) republish the topic using image_transport which is available for ROS2.

`ros2 run image_transport republish raw in:=image_raw compressed out:=image_raw_compressed`


## Dependencies

Make sure to link/install https://github.com/ros-perception/image_transport_plugins/tree/ros2 before to enable compressed image republishing using image_transport since its not included in the base package. More information here http://wiki.ros.org/image_transport, here http://wiki.ros.org/compressed_image_transport and here https://answers.ros.org/question/35183/compressed-image-to-image/

