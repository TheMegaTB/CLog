cmake_minimum_required(VERSION 3.2)
project(CLog)

# Enable the use of the global offset table
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

add_library(${PROJECT_NAME} STATIC src/Logger.cpp src/Logger.hpp)
include_directories(include)
target_include_directories(${PROJECT_NAME} INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
        $<INSTALL_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>)

export(TARGETS ${PROJECT_NAME}
        FILE "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Targets.cmake")
export(PACKAGE ${PROJECT_NAME})

install(FILES "src/Logger.hpp" DESTINATION include/${PROJECT_NAME})
install(FILES "${CMAKE_BINARY_DIR}/libCLog.a" DESTINATION lib/${PROJECT_NAME})
