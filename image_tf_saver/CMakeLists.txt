cmake_minimum_required(VERSION 2.8)
project(image_tf_saver)

find_package(catkin REQUIRED COMPONENTS camera_calibration_parsers cv_bridge dynamic_reconfigure image_transport message_filters message_generation nodelet rosconsole roscpp std_srvs)

catkin_package(CATKIN_DEPENDS dynamic_reconfigure)
find_package(Boost REQUIRED COMPONENTS signals thread)
find_package(OpenCV REQUIRED)

include_directories(${Boost_INCLUDE_DIRS}
                    ${catkin_INCLUDE_DIRS}
                    ${OpenCV_INCLUDE_DIRS}
)

# Extra tools
add_executable(image_saver src/nodes/image_saver.cpp)
target_link_libraries(image_saver ${catkin_LIBRARIES}
                                  ${OpenCV_LIBRARIES}
)

install(TARGETS image_saver
        DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

# Deal with the GUI's
if(ANDROID)
  return()
endif()

find_package(GTK2)
add_definitions(-DHAVE_GTK)
include_directories(${GTK2_INCLUDE_DIRS})
