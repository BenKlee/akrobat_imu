cmake_minimum_required(VERSION 3.5)
project(akrobat_imu)

set(CMAKE_CXX_FLAGS "-std=c++14 ${CMAKE_CXX_FLAGS}")
add_compile_options("-w")

find_package(catkin REQUIRED COMPONENTS
  roscpp
  sensor_msgs
  tf
  tf2
)

catkin_package(
  CATKIN_DEPENDS
    tf
    tf2
    sensor_msgs
    roscpp
)

include_directories(
  ${catkin_INCLUDE_DIRS}
  include
)

add_executable(akrobat_imu
  src/akrobat_imu.cpp
  src/brick_imu_v2.cpp
  src/ip_connection.cpp
)

target_link_libraries(akrobat_imu ${catkin_LIBRARIES})

install(TARGETS akrobat_imu
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY launch
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
