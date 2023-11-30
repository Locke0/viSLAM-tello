# Dockerfile for Turtlebot3 Gazebo Simulation

FROM ubuntu:18.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt update; apt install -y gnupg2

RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros-latest.list' && \
    apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

RUN apt update && \
    apt install -y \
        tmux \
        vim \
        python-pip \
        python-tk \
        python3-vcstool \
        libyaml-dev \
        libgeographic-dev \
        python3-yaml \
        ros-melodic-desktop-full \
        python-rosdep \
        python-rosinstall \
        python-rosinstall-generator \
        python-wstool \
        build-essential \
        ros-melodic-joy \
        ros-melodic-tf2-sensor-msgs \
        ros-melodic-rosbash \
        ros-melodic-rviz \
        ros-melodic-teleop-twist-joy \
        ros-melodic-teleop-twist-keyboard \
        ros-melodic-laser-proc \
        ros-melodic-rgbd-launch \
        ros-melodic-depthimage-to-laserscan \
        ros-melodic-rosserial-arduino \
        ros-melodic-rosserial-python \
        ros-melodic-rosserial-server \
        ros-melodic-rosserial-client \
        ros-melodic-rosserial-msgs \
        ros-melodic-amcl \
        ros-melodic-map-server \
        ros-melodic-move-base \
        ros-melodic-urdf \
        ros-melodic-robot-state-publisher \
        ros-melodic-xacro \
        ros-melodic-compressed-image-transport \
        ros-melodic-rqt-image-view \
        ros-melodic-gmapping \
        ros-melodic-navigation \
        ros-melodic-interactive-markers \
        ros-melodic-codec-image-transport \
        ros-melodic-camera-info-manager-py \
        ros-melodic-pid \
        ros-melodic-geographic-msgs

# Build catkin_ws
RUN mkdir -p /catkin_ws/src && \
    rosdep init && \
    rosdep update


ARG USERNAME=ros
ARG USER_UID=1000
ARG USER_GID=$USER_UID
  
# Create a non-root user
RUN groupadd --gid $USER_GID $USERNAME \
  && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
  # Add sudo support for the non-root user
  && apt-get update \
  && apt-get install -y sudo \
  #FIXME: fix root permissions for better security
  && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
  && chmod 0440 /etc/sudoers.d/$USERNAME \
  && rm -rf /var/lib/apt/lists/*
    
# Set up autocompletion for user
RUN apt-get update && apt-get install -y git-core bash-completion \
  && echo "if [ -f /opt/ros/${ROS_DISTRO}/setup.bash ]; then source /opt/ros/${ROS_DISTRO}/setup.bash; fi" >> /home/$USERNAME/.bashrc \
  && echo "if [ -f /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash ]; then source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash; fi" >> /home//$USERNAME/.bashrc \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /catkin_ws/src
RUN /bin/bash -c "source /opt/ros/melodic/setup.bash; cd /catkin_ws; catkin_make"

#  Source environments
RUN echo "source /opt/ros/melodic/setup.bash" >> /root/.bashrc && \
    echo "source /catkin_ws/devel/setup.bash" >> /root/.bashrc
    

# Cleanup
RUN rm -rf /root/.cache

# Entrypoint
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

WORKDIR /catkin_ws
ENTRYPOINT [ "/entrypoint.sh" ]