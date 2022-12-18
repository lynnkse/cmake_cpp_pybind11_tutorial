cmake_minimum_required(VERSION 3.1)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_FLAGS "-O3")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")
set (PYTHON_VERSION 3.8)

project(automobile)

find_package(Python ${PYTHON_VERSION} REQUIRED COMPONENTS Development)

include_directories("${CMAKE_SOURCE_DIR}/cpp/include/automobile_bits")
include_directories("${CMAKE_SOURCE_DIR}/python")

file (GLOB SOURCE_FILES "cpp/src/*.cpp")
file (GLOB HEADER_FILES "cpp/include/automobile_bits/*.hpp")
file (GLOB PYTHON_FILES "python/*.cpp" "python/*.hpp")

# Set up such that XCode organizes the files

include(pybind11.cmake)
pybind11_add_module(automobile 
	${SOURCE_FILES}
	${HEADER_FILES}
	${PYTHON_FILES}
)

target_link_libraries(automobile PUBLIC)

install(TARGETS automobile
  COMPONENT python
  LIBRARY DESTINATION ${Python_SITELIB}/bike # this installed automobile.so to /bike/ (!)
  )
