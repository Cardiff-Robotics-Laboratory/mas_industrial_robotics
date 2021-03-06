cmake_minimum_required(VERSION 2.8.3)
project(mir_base_placement)

find_package(catkin REQUIRED
  COMPONENTS
    actionlib
    geometry_msgs
    mcr_perception_msgs
    mir_navigation_msgs
    roscpp
    sensor_msgs
)

catkin_package(
  CATKIN_DEPENDS
    geometry_msgs
    mcr_perception_msgs
    mir_navigation_msgs
    sensor_msgs
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)


### EXECUTABLES
add_executable(base_placement_node 
  ros/src/base_placement_node.cpp
)
add_dependencies(base_placement_node
  ${catkin_EXPORTED_TARGETS}
)
target_link_libraries(base_placement_node
  ${catkin_LIBRARIES}
)

add_executable(basescan_orientation_test 
  ros/tools/basescan_orientation_test.cpp
)
add_dependencies(basescan_orientation_test
  ${catkin_EXPORTED_TARGETS}
)
target_link_libraries(basescan_orientation_test
  ${catkin_LIBRARIES}
)


### TESTS
if(CATKIN_ENABLE_TESTING)
  find_package(roslaunch REQUIRED)

  roslaunch_add_file_check(ros/launch)
endif()


### INSTALLS
install(
  TARGETS
    base_placement_node
    basescan_orientation_test
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(PROGRAMS
    ros/mockup/base_placement_node_mockup
    DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY ros/launch/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/ros/launch/
)
