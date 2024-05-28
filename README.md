# Reinforcement Learning for Autonomous Navigation and Dynamic Obstacle Avoidance using Deep Q Network and Twin Delayed DDPG

This repository contains the implementation of autonomous vehicle navigation using reinforcement learning (RL) techniques, specifically focusing on Deep Q-Networks (DQN) and Twin Delayed Deep Deterministic Policy Gradient (TD3) algorithms. The project was conducted using the TurtleBot3 robot in a simulated ROS2 Foxy and Gazebo 11 environment. The primary objective was to train the TurtleBot3 to navigate autonomously through an environment while avoiding moving obstacles.

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Algorithms](#algorithms)
  - [Deep Q-Network (DQN)](#deep-q-network-dqn)
  - [Twin Delayed Deep Deterministic Policy Gradient (TD3)](#twin-delayed-deep-deterministic-policy-gradient-td3)
- [Enhancements and Hyperparameter Tuning](#enhancements-and-hyperparameter-tuning)
- [Results](#results)
- [Contribution](#contribution)
- [Future Work](#future-work)

## Introduction
Autonomous vehicle navigation has become a pivotal area of research in the field of robotics, driven by the potential to enhance safety, efficiency, and accessibility in various domains including transportation, logistics, and personal robotics. This project explores the application of two prominent RL algorithms, Deep Q-Networks (DQN) and Twin Delayed Deep Deterministic Policy Gradient (TD3), for the navigation of a TurtleBot3 robot in a simulated ROS Gazebo environment.

## Features
- Autonomous navigation in a simulated environment using TurtleBot3
- Dynamic and static obstacle avoidance
- Implementation of DQN and TD3 algorithms
- Enhancements such as learning rate scheduler and batch normalization
- Comprehensive hyperparameter tuning
- Comparative analysis of DQN and TD3 performance

## Installation

### **Docker Installation (Recommended)**

In order to greatly simplify the installation process and get up and running quickly it is recommended to use Docker. Docker can be seen as a lightweight VM that allows you to run applications within an isolated container making it easy to install all of the dependencies.

First, [install docker](https://docs.docker.com/engine/install/ubuntu/)

Now, in order to use your GPU within the docker container to run the machine learning models, we need to complete a few extra simple steps.
You should already have the nvidia driver installed on your system.

### **Manual Installation**

If you don't want to use docker you can install all dependencies manually.

### Prerequisites
- Ubuntu 20.04 LTS
- ROS2 Foxy Fitzroy
- Gazebo 11.0
- Python 3.8+
- PyTorch 1.10.0

#### **Installing ROS2**
Install ROS2 foxy according to the following guide: [link](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html). You can choose either the Desktop or Bare Bones ROS installation, both work. <br>
To prevent having to manually source the setup script every time, add the following line at the end of your `~/.bashrc` file:

```
source /opt/ros/foxy/setup.bash
```

More detailed installation instructions can be found [here](https://automaticaddison.com/how-to-install-ros-2-foxy-fitzroy-on-ubuntu-linux/).


#### **Installing Gazebo**

For this project we will be using Gazebo **11.0.** To install Gazebo 11.0, navigate to the following [page](http://gazebosim.org/tutorials?tut=install_ubuntu), select Version 11.0 in the top-right corner and follow the default installation instructions.

Next, we need to install a package that allows ROS2 to interface with Gazebo.
To install this package we simply execute the following command in a terminal:
```
sudo apt install ros-foxy-gazebo-ros-pkgs
```
After successful installation we are now going to test our ROS2 + Gazebo setup by making a demo model move in the simulator. First, install two additional packages for demo purposes (they might already be installed):
```
sudo apt install ros-foxy-ros-core ros-foxy-geometry2
```
Source ROS2 before we launch the demo:
```
source /opt/ros/foxy/setup.bash
```

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/ROBOTIS-GIT/turtlebot3_drlnav.git
   cd turtlebot3_drlnav
   
2. Install dependencies:
   ```bash
   sudo apt update
   sudo apt install python3-pip
   pip3 install -r requirements.txt

4. Setup ROS2 and Gazebo environment:
   ```bash
   source /opt/ros/foxy/setup.bash

## Usage

1. Launch the Gazebo simulation:
   ```bash
   ros2 launch turtlebot3_gazebo turtlebot3

2. Run the training script for DQN:
   ```bash
   python3 train_dqn.py
   
3. Run the training script for TD3:
   ```bash
   python3 train_td3.py

4. Evaluate the trained models:
   ```bash
   python3 evaluate.py

## Algorithms

### Deep Q-Network (DQN)
DQN is a model-free, off-policy RL algorithm that approximates the Q-value function using a deep neural network. The Q-network receives the current state as input and outputs Q-values for all possible actions. The action with the highest Q-value is selected using an ϵ-greedy policy.

### Twin Delayed Deep Deterministic Policy Gradient (TD3)
TD3 is an actor-critic algorithm designed for continuous action spaces. It extends the Deep Deterministic Policy Gradient (DDPG) by addressing overestimation bias and improving learning stability. TD3 uses twin Q-networks to reduce overestimation and delayed policy updates to stabilize training.

## Enhancements and Hyperparameter Tuning
Several enhancements and hyperparameter tuning techniques were employed to improve the performance and stability of both DQN and TD3 algorithms:

- **Learning Rate Scheduler**: Dynamically adjusts the learning rate during training.
- **Batch Normalization**: Stabilizes and accelerates training by normalizing the inputs of each layer.
- **Epsilon Decay (for DQN)**: Balances exploration and exploitation by gradually decreasing the probability of choosing a random action.
- **Target Update Frequency (for DQN)**: Updates the target Q-network at a fixed frequency for more stable target values.
- **Policy Update Frequency (for TD3)**: Updates the policy network less frequently than the Q-networks to prevent destabilizing updates.

## Results
The results of the training processes for both DQN and TD3 algorithms are analyzed based on key metrics such as navigation outcomes (success rate of reaching the goal and collision rates), average network losses, and average rewards. Graphical representations are included to visualize performance differences.

### DQN Algorithm Performance
- **Without Hyperparameter Tuning**: High number of collisions, low success rate, high initial average critic loss with significant variance, unstable average rewards.
- **With Hyperparameter Tuning**: Improved navigation success, reduced collisions, stabilized average critic loss, more consistent upward trend in average rewards.

### TD3 Algorithm Performance
- **Without Hyperparameter Tuning**: High number of collisions, low navigation success, high initial average critic loss with significant variance, unstable average rewards.
- **With Hyperparameter Tuning**: Significant reduction in collisions, higher navigation success, stabilized and lower average critic loss, consistent upward trend in average rewards.

## Contribution
Key contributions made to the project include:

- Integration of a learning rate scheduler for efficient convergence.
- Addition of batch normalization layers for stable and accelerated training.
- Extensive hyperparameter tuning for optimized algorithm performance.
- Comprehensive comparative analysis of DQN and TD3 algorithms.

The code used for training and testing the DQN and TD3 algorithms on TurtleBot3 is available in this repository.

## Future Work
Potential future directions for this project include:

- Extending the algorithms to handle more complex and larger environments.
- Incorporating additional sensors and sensor fusion techniques to enhance perception capabilities.
- Exploring other RL algorithms and hybrid approaches for improved navigation performance.
- Implementing real-world testing on physical TurtleBot3 robots.


For more information, please contact us at:

- Joseph Thomas (joseph10@umd.edu)
- Rishikesh Jadhav (rjadhav1@umd.edu)





   



