cmake_minimum_required(VERSION 2.8.3)
project(myo_master)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -g")

SET(CMAKE_BUILD_TYPE Debug)

## Find catkin and any catkin packages
find_package(catkin REQUIRED COMPONENTS roscpp controller_manager gazebo_ros_control std_msgs)

## Declare a catkin package
catkin_package(CATKIN_DEPENDS message_runtime)

include_directories(
${catkin_INCLUDE_DIRS} 
include/ 
${CMAKE_CURRENT_SOURCE_DIR}/../common_utilities/include
${CMAKE_CURRENT_SOURCE_DIR}/../flexrayusbinterface/include
/usr/include/gazebo-2.2
/usr/include/sdformat-1.4
)

add_executable(multiJoint src/main.cpp src/roboy.cpp
${CMAKE_CURRENT_SOURCE_DIR}/../flexrayusbinterface/src/FlexRayHardwareInterface.cpp)
add_dependencies(multiJoint common_utilities_gencpp)

target_link_libraries(multiJoint ${catkin_LIBRARIES} -lftd2xx -lncurses)
