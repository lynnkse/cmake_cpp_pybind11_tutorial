cmake_minimum_required(VERSION 3.1)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

project(test_cpp)

include_directories(/usr/local/include)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/../bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/../bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/../bin)

find_library(AUTOMOBILE_LIB automobile HINTS /usr/local/lib/) 
#Please set them or make sure they are set and tested correctly in the CMake files:
# AUTOMOBILE_LIB  (!)

add_executable(test_cpp src/test_cpp.cpp)

target_link_libraries(test_cpp PUBLIC ${AUTOMOBILE_LIB})