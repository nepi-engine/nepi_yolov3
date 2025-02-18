cmake_minimum_required(VERSION 2.8.12)
project(nepi_yolov3)

# Set c++11 cmake flags
set(CMAKE_CXX_FLAGS "-std=c++11 -Wall -Wno-unused-result -Wno-unknown-pragmas -Wno-unused-variable -fPIC -fpermissive ${CMAKE_CXX_FLAGS}")

# Define path of yolov3 folder here.
set(YOLOV3_PATH ${CMAKE_CURRENT_SOURCE_DIR}/yolov3)

# Data label images are installed below -- use that location for the compiled-in path to
# avoid being dependent on the source folder at build time
set( YOLOV3_FILE_INSTALL_FOLDER
  # Must hard-code it because CATKIN_GLOBAL_SHARE_DESTINATION is not yet defined at this point
  # ${CATKIN_GLOBAL_SHARE_DESTINATION}/yolov3
  /opt/nepi/ros/share/yolov3
)
message(WARNING "Installing yolov3 files to hard-coded ${YOLOV3_FILE_INSTALL_FOLDER}")
add_definitions(-D YOLOV3_FILE_PATH="${YOLOV3_FILE_INSTALL_FOLDER}")


# Find required packages
find_package(catkin REQUIRED COMPONENTS
std_msgs
)

catkin_package(
  CATKIN_DEPENDS
    rospy
    std_msgs
)


## Mark other files for installation (e.g. launch and bag files, etc.)
set( YOLOV3_INSTALL_FOLDER 
  # Must hard-coded 
  /opt/nepi/ros/share/yolov3
)
install(DIRECTORY   yolov3/
  DESTINATION ${YOLOV3_INSTALL_FOLDER}
  PATTERN "*git*" EXCLUDE
)



