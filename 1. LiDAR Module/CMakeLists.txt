cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

add_definitions(-std=c++11)

set(PCL_DIR "C:/Users/Seymu/vcpkg/installed/x86-windows/share/pcl")
set(EIGEN_INCLUDE_DIR "C:/Users/Seymu/vcpkg/installed/x86-windows/shareeigen3")
set(Boost_INCLUDE_DIR "C:/Users/Seymu/vcpkg/installed/x86-windows/share")
set(CXX_FLAGS "-Wall")
set(CMAKE_CXX_FLAGS, "${CXX_FLAGS}")

project(playback)

find_package(PCL 1.9 REQUIRED common io)

include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})
list(REMOVE_ITEM PCL_LIBRARIES "vtkproj4")


add_executable (environment src/environment.cpp src/render/render.cpp src/processPointClouds.cpp)
target_link_libraries (environment ${PCL_LIBRARIES})