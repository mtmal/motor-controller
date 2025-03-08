cmake_minimum_required(VERSION 3.10)

# set the project name
project(MotorController)

set(CMAKE_CXX_FLAGS "-fPIC -g -pedantic -Wall -Wextra")

# add the I2C submodule
if (CUSTOM_I2C)
    include_directories(${CUSTOM_I2C}/src)
else()
    add_subdirectory(I2C)
    include_directories(I2C/src)
endif()

include_directories(src)

# Build the actual library
add_library(MotorController SHARED src/PCA9685.cpp src/ContinuousServo.cpp)
target_link_libraries(MotorController I2C)
