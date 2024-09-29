# Use the official ROS image
FROM ros:noetic-ros-base

# Install OpenCV and required dependencies
RUN apt-get update && apt-get install -y \
    python3-catkin-tools \
    python3-opencv \
    ros-noetic-cv-bridge \
    && rm -rf /var/lib/apt/lists/*

# Create the vscode user
RUN useradd -m vscode

# Set up a workspace
RUN mkdir -p /catkin_ws/src
WORKDIR /catkin_ws/src

# Copy your package to the workspace
COPY . /catkin_ws/src/my_camera_package/

# Build the workspace
WORKDIR /catkin_ws
RUN /bin/bash -c "source /opt/ros/noetic/setup.bash && catkin_make"

# Set the entry point for the ROS node
CMD ["/bin/bash", "-c", "source /opt/ros/noetic/setup.bash && source devel/setup.bash && rosrun my_camera_package camera_node.py"]
