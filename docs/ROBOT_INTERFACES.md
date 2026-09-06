# Robot interfaces — documentation only, runtime verification pending

Source: official main README and gripper_command_clamp.py; PDF for ERC output topics. No ROS system is running.

| Interface | Documented name/type |
|---|---|
| Base command | /cmd_vel — geometry_msgs/msg/Twist |
| Odometry | /odom — nav_msgs/msg/Odometry |
| TF | Discover /tf, /tf_static and actual frame tree in runtime |
| RGB | /head_front_camera/head_front_camera/color/image_raw — sensor_msgs/msg/Image |
| RGB calibration | /head_front_camera/head_front_camera/color/camera_info — sensor_msgs/msg/CameraInfo |
| Depth | /head_front_camera/head_front_camera/depth/image_rect_raw — sensor_msgs/msg/Image (float32 documented) |
| Depth calibration | /head_front_camera/head_front_camera/depth/camera_info — sensor_msgs/msg/CameraInfo |
| Point cloud | /head_front_camera/head_front_camera/depth/color/points — sensor_msgs/msg/PointCloud2 |
| LiDAR | /scan_front_raw, /scan_rear_raw — sensor_msgs/msg/LaserScan |
| IMU | /base_imu — sensor_msgs/msg/Imu |
| Contacts | /contacts, /bin_contacts — ros_gz_interfaces/msg/Contacts |
| Arms | /arm_left_controller/joint_trajectory, /arm_right_controller/joint_trajectory — trajectory_msgs/msg/JointTrajectory |
| Grippers, PUBLIC | /gripper_left_controller/joint_trajectory, /gripper_right_controller/joint_trajectory |
| Grippers, INTERNAL | same names with controller_raw: do not bypass range relay |
| Head/torso | /head_controller/joint_trajectory, /torso_controller/joint_trajectory |
| Joint feedback | /joint_states — inspect runtime message/interfaces |
| Competition | /erc/shelf_column_identification, /erc/shelf_row_identification — std_msgs/msg/Int32 |

Gripper relay source accepts public trajectory topics and forwards valid points to raw controllers; bounds 0–0.069, out-of-range points rejected. README controller table shows raw names but examples show public names. Do not assume public follow_joint_trajectory actions exist. Runtime discovery decides valid arm/gripper action paths. No arm selected yet.

Joint names: arm_left_1_joint..7, arm_right_1_joint..7; gripper_left_finger_joint / gripper_right_finger_joint; head_1_joint/head_2_joint; torso_lift_joint.

Documented nominal sensors: RGB/depth 640x360 at 30 Hz; depth 0.2–8 m; LiDAR 10 Hz, 818 samples, ~270 degrees each; IMU 100 Hz. These are configuration values, not measured performance.

After simulator launch save topic list (-t too), nodes, services, actions, ros2 control list_controllers/list_hardware_interfaces, param list and tf2_tools view_frames. Inspect rates and one message for each relevant sensor. Record TF/calibration/QoS, contact structure and actual controller feedback. Inspect MoveIt packages/SRDF/planning groups/scene/actions and Nav2 lifecycle/configuration; installed does not mean operational.
