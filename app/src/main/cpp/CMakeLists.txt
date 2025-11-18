cmake_minimum_required(VERSION 3.22.1)

project("yolov12")

# ============================================================
# Android NDK setup
# ============================================================
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_definitions(-DANDROID_NDK)

# ============================================================
# OpenCV
# ============================================================
set(OpenCV_DIR ${CMAKE_SOURCE_DIR}/3rdparty/opencv/sdk/native/jni)
find_package(OpenCV REQUIRED)

# For older OpenCV packages that don’t auto-link
include_directories(${OpenCV_INCLUDE_DIRS})

# ============================================================
# NCNN
# ============================================================
set(ncnn_DIR ${CMAKE_SOURCE_DIR}/3rdparty/ncnn/arm64-v8a/lib/cmake/ncnn)
find_package(ncnn REQUIRED)

include_directories(${ncnn_INCLUDE_DIRS})

# ============================================================
# Source files
# ============================================================
add_library(${CMAKE_PROJECT_NAME} SHARED
        ndkcamera.cpp
        yolo.cpp
        native-lib.cpp
)

# ============================================================
# Android system libs
# ============================================================
find_library(log-lib log)
find_library(android-lib android)
find_library(camera-lib camera2ndk)
find_library(media-lib mediandk)

# ============================================================
# Link everything
# ============================================================
target_link_libraries(
        ${CMAKE_PROJECT_NAME}
        ncnn
        ${OpenCV_LIBS}
        ${camera-lib}
        ${media-lib}
        ${android-lib}
        ${log-lib}
)
