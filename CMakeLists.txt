cmake_minimum_required(VERSION 3.8)
project(message)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(builtin_interfaces REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED) 


FILE(GLOB_RECURSE message  RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "*.msg")

# set(message
#   "msg/ImuData.msg"
#   "msg/ImuDataFrame.msg"
#   "msg/ImuAcceleration.msg"
#   "msg/ImuAngularVelocity.msg"
#   "msg/ImuAngular.msg"
# )
set(message ${message})
rosidl_generate_interfaces(
  ${PROJECT_NAME} ${message} 
  DEPENDENCIES builtin_interfaces std_msgs   
)

ament_export_dependencies(rosidl_default_generators)
ament_export_dependencies(rosidl_default_runtime)
ament_export_include_directories(include) 
ament_package()  

# colcon build --packages-select message