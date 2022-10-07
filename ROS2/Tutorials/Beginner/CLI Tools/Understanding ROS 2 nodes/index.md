# Understanding ROS 2 nodes

- **ROS graph:** It is a network of ROS 2 elements processing data together at one time.
    - It encompasses all executables and the connections between them.

- Nodes:
    - Each node is responsible for a single, module purpose.
    - Each node can send and receive data to other nodes via topic, services, actions, or parameters.
    - In ROS 2, a single executable (C++ program, Python program, etc.) can contain one or more nodes.
