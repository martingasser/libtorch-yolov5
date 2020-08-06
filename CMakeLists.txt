cmake_minimum_required(VERSION 3.5.1)
project(libtorch-yolov5)

# Try to find OpenCV
# set(OpenCV_DIR ....)
find_package(OpenCV REQUIRED)
if (OpenCV_FOUND)
    # If the package has been found, several variables will
    # be set, you can find the full list with descriptions
    # in the OpenCVConfig.cmake file.
    # Print some message showing some of them
    message(STATUS "OpenCV library status:")
    message(STATUS "    version: ${OpenCV_VERSION}")
    message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}" \n)
else ()
    message(FATAL_ERROR "Could not locate OpenCV" \n)
endif()

set(Torch_DIR ../../libtorch_1_6_0/share/cmake/Torch/)
find_package(Torch REQUIRED)
if (Torch_FOUND)
    message(STATUS "Torch library found!")
    message(STATUS "    include path: ${TORCH_INCLUDE_DIRS}" \n)
else ()
    message(FATAL_ERROR "Could not locate Torch" \n)
endif()

include_directories(${PROJECT_SOURCE_DIR}/include)

file(GLOB SOURCE_FILES src/*.cpp)

add_executable(${CMAKE_PROJECT_NAME} ${SOURCE_FILES})

target_link_libraries (
        ${CMAKE_PROJECT_NAME}
        ${TORCH_LIBRARIES}
        ${OpenCV_LIBS}
)

set_property(TARGET ${CMAKE_PROJECT_NAME} PROPERTY CXX_STANDARD 14)