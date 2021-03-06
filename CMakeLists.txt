cmake_minimum_required(VERSION 2.8)
project(quadprog CXX)

set(CMAKE_BUILD_TYPE Release)

if(MSVC)
    set(LIB_TYPE "STATIC")
    set(suffix_type "_static")
    set(install_type "ARCHIVE")
else()
    set(LIB_TYPE "SHARED")
    set(suffix_type "")
    if(UNIX)
        set(install_type "LIBRARY")
    else()
        set(install_type "RUNTIME")
    endif()
endif()

# Check dependencies
find_package(PkgConfig REQUIRED)
PKG_CHECK_MODULES(PC_EIGEN eigen3 REQUIRED)
if(NOT PC_EIGEN_FOUND)
    message("Failed to detect Eigen, check PKG_CONFIG_PATH." )
endif(NOT PC_EIGEN_FOUND)

add_subdirectory(pkg-config)
add_subdirectory(include)
add_subdirectory(src)
