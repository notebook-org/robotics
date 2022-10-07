- ROS 2 relies on the notion of combining workspaces using the shell environment.
    - **Workspace:**  Location on your system where you are developing with ROS 2.
        - Core workspace is called the **underlay**.
        - Subsequent local workspace are called **overlay**.
        - Combining workspaces makes developing against different versions of ROS 2, or against different sets of packages, easier.
        - It also allows the installation of several ROS 2 distributions on the same computer and switching between them.
        - This is accomplished by sourcing setup files every time you open a new shell.

## The ROS_DOMAIN_ID
- In DDS, the primary mechanism for having different logical networks share a physical network is known as the Domain ID.
- ROS 2 nodes on the same domain can freely discover and send messages to each other, while ROS 2 nodes on different domains cannot.
- All ROS 2 nodes use domain ID 0 by default.
