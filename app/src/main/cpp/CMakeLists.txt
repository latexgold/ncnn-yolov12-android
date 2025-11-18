cmake_minimum_required(VERSION 3.22.1)

project("yolov12")

# OpenCV
set(OpenCV_DIR ${CMAKE_SOURCE_DIR}/3rdparty/opencv/sdk/native/jni)
find_package(OpenCV REQUIRED)

# NCNN
set(ncnn_DIR ${CMAKE_SOURCE_DIR}/3rdparty/ncnn/arm64-v8a/lib/cmake/ncnn)
find_package(ncnn REQUIRED)

add_library(${CMAKE_PROJECT_NAME} SHARED
        ndkcamera.cpp
        yolo.cpp
        native-lib.cpp)

target_link_libraries(${CMAKE_PROJECT_NAME}
        ncnn
        ${OpenCV_LIBS}
        camera2ndk
        mediandk
        android
        log)
