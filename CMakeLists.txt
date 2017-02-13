cmake_minimum_required(VERSION 3.6)
project(CLog)

add_library(${PROJECT_NAME} include/Logger.hpp src/Logger.cpp)
include_directories(include)
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

install(FILES "include/Logger.hpp" DESTINATION include/${PROJECT_NAME})