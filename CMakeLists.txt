cmake_minimum_required(VERSION 2.8.3)
project(tire_sim_plugin)

## Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  gazebo_ros
  gazebo_dev
  gazebo_msgs
)

# Depend on system install of Gazebo
find_package(gazebo REQUIRED)

link_directories(${GAZEBO_LIBRARY_DIRS})

include_directories(
  include
  ${Boost_INCLUDE_DIR}
  ${catkin_INCLUDE_DIRS}
  ${GAZEBO_INCLUDE_DIRS}
  ${OGRE_INCLUDE_DIRS}
)

###########
## Build ##
###########

## Declare a C++ library
add_library(${PROJECT_NAME}
  src/TireFrictionPlugin.cpp
)

## Specify libraries to link a library or executable target against
target_link_libraries(${PROJECT_NAME}
  ${catkin_LIBRARIES} ${GAZEBO_LIBRARIES}
)

catkin_package(
  DEPENDS roscpp gazebo_ros
  CATKIN_DEPENDS roscpp gazebo_ros
  INCLUDE_DIRS include
)
