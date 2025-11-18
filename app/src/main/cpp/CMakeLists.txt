cmake_minimum_required(VERSION 3.22.1)

project(yolov12)

# The path is now RELATIVE, not E:/....
set(OpenCV_DIR ${CMAKE_SOURCE_DIR}/opencv/sdk/native/jni)
find_package(OpenCV REQUIRED)

set(ncnn_DIR ${CMAKE_SOURCE_DIR}/ncnn/${ANDROID_ABI}/lib/cmake/ncnn)
find_package(ncnn REQUIRED)

add_library(${CMAKE_PROJECT_NAME} SHARED
        ndkcamera.cpp
        ndkcamera.h
        yolo.cpp
        yolo.h
        native-lib.cpp
)

include_directories(
        ${OpenCV_INCLUDE_DIRS}
        ${ncnn_INCLUDE_DIRS}
)

target_link_libraries(${CMAKE_PROJECT_NAME}
        ${OpenCV_LIBS}
        ncnn
        camera2ndk
        mediandk
        android
        log
)
