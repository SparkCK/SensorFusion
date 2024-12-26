cmake_minimum_required(VERSION 2.8 FATAL_ERROR)
project(playback)

add_definitions(-std=c++14)

# set(PCL_DIR "C:/Users/Seymu/vcpkg/installed/x86-windows/share/pcl")
# set(EIGEN_INCLUDE_DIR "C:/Users/Seymu/vcpkg/installed/x86-windows/shareeigen3")
# set(Boost_INCLUDE_DIR "C:/Users/Seymu/vcpkg/installed/x86-windows/share")
# set(CXX_FLAGS "-Wall")
# set(CMAKE_CXX_FLAGS, "${CXX_FLAGS}")

set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -O3")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -Wall -O0 -g -ggdb")


find_package(PCL 1.12 REQUIRED visualization segmentation common io)
find_package(Boost 1.65.0 REQUIRED COMPONENTS filesystem)

include_directories(
    ${PCL_INCLUDE_DIRS}
    ${Boost_INCLUDE_DIRS}
    ${CMAKE_CURRENT_SOURCE_DIR}/src
)

link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

list(REMOVE_ITEM PCL_LIBRARIES "vtkproj4") # remove vtkproj4 from PCL_LIBRARIES


add_executable(environment src/environment.cpp src/processPointClouds.cpp src/render/render.cpp)

target_link_libraries (environment
    ${PCL_LIBRARIES}
    ${Boost_LIBRARIES}
)