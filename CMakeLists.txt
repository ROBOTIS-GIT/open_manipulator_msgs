################################################################################
# Set minimum required version of cmake, project name and compile options
################################################################################
cmake_minimum_required(VERSION 3.5)
project(open_manipulator_msgs)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

################################################################################
# Find ament packages and libraries for ament and system dependencies
################################################################################
find_package(ament_cmake REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED)

################################################################################
# Declare ROS messages, services and actions
################################################################################
set(msg_files
  "msg/JointPosition.msg"
  "msg/KinematicsPose.msg"
  "msg/OpenManipulatorState.msg"
)

set(srv_files
  "srv/GetJointPosition.srv"
  "srv/GetKinematicsPose.srv"
  "srv/SetJointPosition.srv"
  "srv/SetKinematicsPose.srv"
  "srv/SetDrawingTrajectory.srv"
  "srv/SetActuatorState.srv"
)

rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  ${srv_files}
  DEPENDENCIES std_msgs geometry_msgs
  ADD_LINTER_TESTS
)

################################################################################
# Macro for ament package
################################################################################
ament_export_dependencies(geometry_msgs)
ament_export_dependencies(rosidl_default_runtime)
ament_export_dependencies(std_msgs)
ament_package()
