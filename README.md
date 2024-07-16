# harpia_simulator
This repository is intended to store the simulation related packages of the UFRJ Nautilus drone
=======
# Harpia Simulator

## Arena Robocup 2023

- Ros 2
- Gazebo multi-robot simulator, version 11.11.0

---

Create a script inside ``/opt/ros/foxy/share/arena23_launch_path`` capable of launching the gazebo simulation world called 'arena23'.

```bash
mkdir /opt/ros/foxy/share/arena23_launch_path && vim /opt/ros/foxy/share/arena23_launch_path/arena23.launch.py
```

```python
import os
from ament_index_python.packages import get_package_share_directory
from launch import LaunchDescription
from launch.actions import IncludeLaunchDescription
from launch.launch_description_sources import PythonLaunchDescriptionSource

def generate_launch_description():
    arena_pkg_dir = get_package_share_directory('harpia_simulator')
    arena23_launch_path = os.path.join(arena_pkg_dir, 'launch')

    arena_world_cmd = IncludeLaunchDescription(
        PythonLaunchDescriptionSource([arena23_launch_path, '/arena23.launch.py'])
    )

    ld = LaunchDescription()

    ld.add_action(arena_world_cmd)

    return ld
```

---
Run

    rosdep install --from-paths . --ignore-src -r -y

Compile and install harpia_simulator package:

    colcon build
