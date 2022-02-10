cmake_minimum_required(VERSION 3.4.1)

project(rknn_yolov5_demo_linux)

set(CMAKE_SYSTEM_NAME Linux)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

if (CMAKE_C_COMPILER MATCHES "aarch64")
  set(LIB_ARCH lib64)
else()
  set(LIB_ARCH lib)
endif()

# drm
set(DRM_DIR ${CMAKE_SOURCE_DIR})
include_directories(${DRM_DIR}/include)
include_directories(${DRM_DIR}/include/libdrm)

include_directories(${CMAKE_SOURCE_DIR}/include)
# rknn api
set(RKNN_API_PATH ${CMAKE_SOURCE_DIR})
include_directories(${RKNN_API_PATH}/include)
set(RKNN_API_LIB ${RKNN_API_PATH}/libs/librknn_api.so)


INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/include)
LINK_DIRECTORIES(${PROJECT_SOURCE_DIR}/libs)
set(link_libs rknn_api pthread opencv_imgproc opencv_highgui opencv_videoio opencv_core opencv_imgcodecs)

set(CMAKE_INSTALL_RPATH "lib")

add_executable(rknn_yolov5_demo
        src/drm_func.c
        src/postprocess.cc
        src/main.cc
        )

set(link_libs rknn_api ${OpenCV_LIBRARIES} pthread ${link_libs})

target_link_libraries(rknn_yolov5_demo
  ${link_libs}
  dl
)

# install target and libraries
set(CMAKE_INSTALL_PREFIX ${CMAKE_SOURCE_DIR}/install/rknn_yolov5_demo)
install(TARGETS rknn_yolov5_demo DESTINATION ./)
install(DIRECTORY model DESTINATION ./)
install(PROGRAMS ${RKNN_API_LIB} DESTINATION lib)
