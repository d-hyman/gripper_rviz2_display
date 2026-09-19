# gripper_assem

ROS 2 package that imports, configures, and visualizes the `gripper_assem` gripper assembly. It provides the URDF model, mesh files, and RViz2 launch scripts needed to quickly preview the gripper's kinematics and joints.

## Overview

This package contains:
- A URDF description of the gripper, generated from SolidWorks via the SW2URDF exporter.
- STL mesh files for each link, used for visual and collision geometry.
- An RViz2 config and launch file that load the gripper model and let you drive its joints interactively via slider controls.

When the launch script is run, RViz2 opens showing the gripper model alongside a `joint_state_publisher_gui` window. Dragging a slider in that window moves the corresponding joint live in the RViz2 view.

This package is a template copied from `robot_arm_assem_v5` — the URDF, CSV, and mesh files are placeholders to be filled in with the gripper's own exported content (see `urdf/gripper_assem.urdf` and `meshes/README.md` for exactly where each piece goes).

## Package contents

```
gripper_assem/
├── config/
│   ├── joint_names_gripper_assem.yaml   # joint name list (placeholder)
│   └── urdf.rviz                        # RViz2 display configuration
├── launch/
│   └── display.launch.py                # ROS 2 launch file
├── meshes/                               # STL meshes
└── urdf/
    ├── gripper_assem.urdf               # robot description (skeleton)
    └── gripper_assem.csv                # SolidWorks export reference data (header only)
```

## Dependencies

- ROS 2 (e.g. Humble or Jazzy)
- `robot_state_publisher`
- `rviz2`
- `joint_state_publisher_gui`

Install the ROS 2 dependencies:

```bash
sudo apt install ros-<distro>-robot-state-publisher ros-<distro>-rviz2 ros-<distro>-joint-state-publisher-gui
```

Replace `<distro>` with your ROS 2 distribution name (e.g. `humble`, `jazzy`).

## Build

From the root of your colcon workspace (e.g. `~/robotic_arm`):

```bash
colcon build --packages-select gripper_assem
source install/setup.bash
```

## Usage

Launch the visualization:

```bash
ros2 launch gripper_assem display.launch.py
```

This starts:
- `robot_state_publisher` — publishes the robot's TF tree from the URDF
- `joint_state_publisher_gui` — opens a window with a slider per joint
- `rviz2` — opens with the `config/urdf.rviz` configuration

Drag any slider in the `joint_state_publisher_gui` window to move the corresponding joint and see the update reflected live in RViz2.
