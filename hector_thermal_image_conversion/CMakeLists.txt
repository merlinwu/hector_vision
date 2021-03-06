cmake_minimum_required(VERSION 2.8.3)
project(hector_thermal_image_conversion)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  cv_bridge
  geometry_msgs
  image_geometry
  image_transport
  pcl_ros
  roscpp
  sensor_msgs
  tf
  tf_conversions
  eigen_conversions
)

find_package(OpenCV REQUIRED)


include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
)
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES hotspot_proc
#  CATKIN_DEPENDS cv_bridge geometry_msgs image_geometry image_transport pcl_ros roscpp sensor_msgs tf
#  DEPENDS system_lib
)

add_library(heat_image_translator src/heat_image_translator.cpp)
#add_dependencies(heat_image_translator ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(heat_image_translator ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})

add_executable(heat_image_translator_node src/heat_image_translator_node.cpp)
target_link_libraries(heat_image_translator_node heat_image_translator)

add_library(heat_image_translator_nodelet src/heat_image_translator_nodelet.cpp)
target_link_libraries(heat_image_translator_nodelet heat_image_translator)

#add_dependencies(hotspot_detector_node ${${PROJECT_NAME}_EXPORTED_TARGETS})

## Specify libraries to link a library or executable target against
