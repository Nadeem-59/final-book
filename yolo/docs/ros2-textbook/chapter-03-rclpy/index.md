---
sidebar_position: 1
---

# Chapter 3: rclpy - Python Client for ROS 2

This chapter focuses on `rclpy`, the Python client library for ROS 2, and how it facilitates the integration of Python-based agents with ROS 2 controllers. `rclpy` allows developers to write ROS 2 nodes in Python, leveraging Python's rich ecosystem for AI, machine learning, and rapid prototyping while benefiting from ROS 2's robust communication framework.

## Connecting Python Agents to ROS 2 Controllers with `rclpy`

`rclpy` provides a straightforward API to interact with ROS 2 primitives like nodes, topics, services, and parameters. This makes it ideal for developing high-level control logic, data processing, and AI applications that need to interface with a robot's hardware controllers via ROS 2.

### Creating a Simple ROS 2 Node in Python

Here's a basic example demonstrating how to create a ROS 2 node using `rclpy` that publishes a simple string message.

```python
import rclpy
from rclpy.node import Node
from std_msgs.msg import String

class MinimalPublisher(Node):
    def __init__(self):
        super().__init__('minimal_publisher')
        self.publisher_ = self.create_publisher(String, 'topic', 10)
        timer_period = 0.5  # seconds
        self.timer = self.create_timer(timer_period, self.timer_callback)
        self.i = 0

    def timer_callback(self):
        msg = String()
        msg.data = 'Hello, ROS 2 from Python! %d' % self.i
        self.publisher_.publish(msg)
        self.get_logger().info('Publishing: "%s"' % msg.data)
        self.i += 1

def main(args=None):
    rclpy.init(args=args)
    minimal_publisher = MinimalPublisher()
    rclpy.spin(minimal_publisher)
    minimal_publisher.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

### Subscribing to a Topic

Nodes can also subscribe to topics to receive data.

```python
import rclpy
from rclpy.node import Node
from std_msgs.msg import String

class MinimalSubscriber(Node):
    def __init__(self):
        super().__init__('minimal_subscriber')
        self.subscription = self.create_subscription(
            String,
            'topic',
            self.listener_callback,
            10)
        self.subscription  # prevent unused variable warning

    def listener_callback(self, msg):
        self.get_logger().info('I heard: "%s"' % msg.data)

def main(args=None):
    rclpy.init(args=args)
    minimal_subscriber = MinimalSubscriber()
    rclpy.spin(minimal_subscriber)
    minimal_subscriber.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```
