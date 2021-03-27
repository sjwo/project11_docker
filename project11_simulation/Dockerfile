FROM ros:noetic-ros-base

RUN export DEBIAN_FRONTEND=noninteractive && apt update && apt upgrade && apt install -y git python3-rosdep python3-vcstool keyboard-configuration python-is-python3 && apt clean

# Create field user and add passwordless sudo rights
RUN useradd --create-home --shell /bin/bash field && adduser field sudo && echo "ALL ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER field

WORKDIR /home/field

RUN mkdir -p project11/catkin_ws/src

RUN git clone https://github.com/rolker/project11.git project11/catkin_ws/src/project11/

RUN rosdep update

RUN vcs import --input project11/catkin_ws/src/project11/config/repos/sim_demo.repos project11/catkin_ws/src/

RUN export DEBIAN_FRONTEND=noninteractive && rosdep install --from-paths project11/catkin_ws/src --ignore-src -r -y

RUN /bin/bash -c ". /opt/ros/noetic/setup.bash && cd project11/catkin_ws && catkin_make"

