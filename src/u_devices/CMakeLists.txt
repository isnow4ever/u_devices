cmake_minimum_required(VERSION 2.8.3)
project(u_devices)

find_package(catkin REQUIRED COMPONENTS  roscpp  rospy  std_msgs)

###################################
## catkin specific configuration ##
###################################
catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS roscpp rospy std_msgs
)

#############
## includes ##
#############

include_directories(include)
include_directories(${catkin_INCLUDE_DIRS})


#############
##  Build  ##
#############
# add_executable(joystick src/devices.h src/joystick.cpp)
# target_link_libraries(joystick arduino ${catkin_LIBRARIES})

# add_executable(keypad src/devices.h src/keypad.cpp)
# target_link_libraries(keypad arduino ${catkin_LIBRARIES})
add_library(gpio_lib src/gpio_lib.h src/gpio_lib.c)
add_library(spi_lib src/spi_lib.h src/spi_lib.c)

add_library(marsboard src/spi_lib.h src/gpio_lib.h src/marsboard.h src/gpio.c src/spi.c)
target_link_libraries(marsboard gpio_lib spi_lib ${catkin_LIBRARIES})

add_executable(io src/marsboard.h src/test.cpp)
target_link_libraries(io marsboard ${catkin_LIBRARIES})

#############
## Install ##
#############
