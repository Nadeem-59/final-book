---
sidebar_position: 4
---

# Lesson 3: Understanding URDF for Humanoids

The **Unified Robot Description Format (URDF)** is an XML format used in ROS to describe the physical structure of a robot. It defines the robot's links, joints, and their relationships.

## Key Components of a URDF File

- **`<robot>`**: The root element of the URDF file.
- **`<link>`**: Describes a rigid part of the robot. It has properties like `name`, `<inertial>`, `<visual>`, and `<collision>`.
- **`<joint>`**: Describes the connection between two links. It has properties like `name`, `type` (e.g., `revolute`, `continuous`, `prismatic`, `fixed`), `<parent>`, `<child>`, and `<axis>`.

## Example: A Simple Two-Link Arm

Here is a simplified URDF for a two-link arm, which could be part of a humanoid robot.

```xml
<?xml version="1.0"?>
<robot name="simple_arm">

  <!-- Base Link -->
  <link name="base_link">
    <visual>
      <geometry>
        <cylinder length="0.2" radius="0.1"/>
      </geometry>
    </visual>
  </link>

  <!-- Shoulder Joint -->
  <joint name="shoulder_joint" type="revolute">
    <parent link="base_link"/>
    <child link="upper_arm_link"/>
    <origin xyz="0 0 0.1"/>
    <axis xyz="0 1 0"/>
  </joint>

  <!-- Upper Arm Link -->
  <link name="upper_arm_link">
    <visual>
      <geometry>
        <box size="0.5 0.1 0.1"/>
      </geometry>
    </visual>
  </link>

</robot>
```

This URDF defines a `base_link` and an `upper_arm_link`, connected by a `shoulder_joint` that allows rotation around the Y-axis. This is the fundamental building block for describing more complex humanoid robots.
