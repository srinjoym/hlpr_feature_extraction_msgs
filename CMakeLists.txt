cmake_minimum_required(VERSION 2.8.3)
project(hlpr_feature_extraction)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -march=native")
set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -Wl,--as-needed")

set(OPENNI_INCLUDE_DIRS /usr/include/ni)
set(ROS_DISTRO indigo)
set(ROS_LIBRARIES /opt/ros/${ROS_DISTRO}/lib/libroscpp.so
        /opt/ros/${ROS_DISTRO}/lib/libroscpp_serialization.so
        /opt/ros/${ROS_DISTRO}/lib/librosconsole.so
        /opt/ros/${ROS_DISTRO}/lib/libroslib.so
        /opt/ros/${ROS_DISTRO}/lib/librostime.so
        /opt/ros/${ROS_DISTRO}/lib/libtf2.so
        /opt/ros/${ROS_DISTRO}/lib/libtf2_ros.so)


#find_package(catkin REQUIRED COMPONENTS dynamic_reconfigure message_generation roscpp std_msgs geometry_msgs)
find_package(OpenCL QUIET)
IF(OpenCL_FOUND)
	SET(LIBRARIES
		${OpenCL_LIBRARIES}
		${LIBRARIES}
	)
ENDIF(OpenCL_FOUND)
find_package(catkin REQUIRED COMPONENTS message_generation roscpp std_msgs geometry_msgs)


add_message_files(
  FILES
  PcFeatures.msg
  PcFeatureArray.msg
)

generate_messages(
  DEPENDENCIES
  std_msgs
  geometry_msgs
)

#generate_dynamic_reconfigure_options(
#  cfg/segmentation.cfg
#)

catkin_package(
 # CATKIN_DEPENDS dynamic_reconfigure message_runtime roscpp std_msgs geometry_msgs
  CATKIN_DEPENDS message_runtime roscpp std_msgs geometry_msgs
)
