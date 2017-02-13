cmake_minimum_required(VERSION 3.6)
project(CLog)

add_library(${PROJECT_NAME} INTERFACE)
include_directories(include)
target_include_directories(${PROJECT_NAME} INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
        $<INSTALL_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>)

install(FILES "include/Logger.hpp" DESTINATION include/${PROJECT_NAME})