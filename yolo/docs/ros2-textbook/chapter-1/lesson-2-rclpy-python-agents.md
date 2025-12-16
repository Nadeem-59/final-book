---
sidebar_position: 3
---

# Lesson 2: Bridging Python Agents to ROS 2 with rclpy

`rclpy` is the official Python client library for ROS 2. It allows you to write ROS 2 nodes in Python, enabling you to integrate your Python-based AI agents, scripts, and applications with a ROS 2 system.

## Key Concepts

- **Initialization**: Before you can use `rclpy`, you must initialize it. This is typically done with `rclpy.init()`.
- **Creating a Node**: You can create a node by inheriting from the `rclpy.node.Node` class.
- **Publishers and Subscribers**: You can create publishers and subscribers using `self.create_publisher()` and `self.create_subscription()` within your node class.
- **Spinning the Node**: To keep your node running and processing callbacks, you need to "spin" it. This can be done with `rclpy.spin(node)`.

## Example: A Simple Publisher Node

Here is a basic example of a Python node that publishes a "Hello, World!" message to a topic.

```python
import rclpy
from rclpy.node import Node
from std_msgs.msg import String

class HelloWorldPublisher(Node):
    def __init__(self):
        super().__init__('hello_world_publisher')
        self.publisher_ = self.create_publisher(String, 'hello_world', 10)
        timer_period = 0.5  # seconds
        self.timer = self.create_timer(timer_period, self.timer_callback)
        self.i = 0

    def timer_callback(self):
        msg = String()
        msg.data = f'Hello, World! {self.i}'
        self.publisher_.publish(msg)
        self.get_logger().info(f'Publishing: "{msg.data}"')
        self.i += 1

def main(args=None):
    rclpy.init(args=args)
    hello_world_publisher = HelloWorldPublisher()
    rclpy.spin(hello_world_publisher)
    hello_world_publisher.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```
