cmake_minimum_required(VERSION 2.8)
project(cv_bridge3)

find_package(catkin REQUIRED COMPONENTS rosconsole sensor_msgs)

if(NOT ANDROID)
find_package(Boost REQUIRED python)
else()
find_package(Boost REQUIRED)
endif()
find_package(OpenCV 3.1.0 REQUIRED)
#set(OpenCV_INCLUDE_DIRS /opt/ros/indigo/include/opencv-3.1.0-dev)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${cv_bridge3}
  CATKIN_DEPENDS rosconsole sensor_msgs
  DEPENDS OpenCV
)

catkin_python_setup()

include_directories(SYSTEM ${Boost_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS})
include_directories(include ${catkin_INCLUDE_DIRS})

if(NOT ANDROID)
add_subdirectory(python)
endif()
add_subdirectory(src)
if(CATKIN_ENABLE_TESTING)
  add_subdirectory(test)
endif()

# install the include folder
install(
  DIRECTORY include/${cv_bridge3}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)
