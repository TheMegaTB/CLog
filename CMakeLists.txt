
cmake_minimum_required(VERSION 3.0)

# define the project
project(CLog VERSION 0.0.1 LANGUAGES CXX)

# define project variables
set(CLOG_TARGET_NAME ${PROJECT_NAME})
set(CLOG_PACKAGE_NAME ${CLOG_TARGET_NAME})
set(CLOG_TARGETS_FILENAME "${CLOG_PACKAGE_NAME}Targets.cmake")
set(CLOG_CONFIG_FILENAME "${CLOG_PACKAGE_NAME}Config.cmake")
set(CLOG_CONFIGVERSION_FILENAME "${CLOG_PACKAGE_NAME}ConfigVersion.cmake")
set(CLOG_CONFIG_DESTINATION "cmake")
set(CLOG_INCLUDE_DESTINATION "include/clog")

# create and configure the library target
add_library(${CLOG_TARGET_NAME} INTERFACE)
target_include_directories(${CLOG_TARGET_NAME} INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
        $<INSTALL_INTERFACE:${CLOG_INCLUDE_DESTINATION}>)

# generate a config and config version file for the package
include(CMakePackageConfigHelpers)
configure_package_config_file("cmake/config.cmake.in"
        "${CMAKE_CURRENT_BINARY_DIR}/${CLOG_CONFIG_FILENAME}"
        INSTALL_DESTINATION ${CLOG_CONFIG_DESTINATION}
        PATH_VARS CLOG_INCLUDE_DESTINATION)
write_basic_package_version_file("${CMAKE_CURRENT_BINARY_DIR}/${CLOG_CONFIGVERSION_FILENAME}"
        VERSION ${PROJECT_VERSION}
        COMPATIBILITY SameMajorVersion)

# export the library target and store build directory in package registry
export(TARGETS ${CLOG_TARGET_NAME}
        FILE "${CMAKE_CURRENT_BINARY_DIR}/${CLOG_TARGETS_FILENAME}")
export(PACKAGE ${CLOG_PACKAGE_NAME})

# install library target and config files
#install(TARGETS ${CLOG_TARGET_NAME}
#        EXPORT ${CLOG_PACKAGE_NAME})
#install(FILES "src/Logger.hpp"
#        DESTINATION ${CLOG_INCLUDE_DESTINATION})
#install(EXPORT ${CLOG_PACKAGE_NAME}
#        FILE ${CLOG_TARGETS_FILENAME}
#        DESTINATION ${CLOG_CONFIG_DESTINATION})
#install(FILES "${CMAKE_CURRENT_BINARY_DIR}/${CLOG_CONFIG_FILENAME}"
#        "${CMAKE_CURRENT_BINARY_DIR}/${CLOG_CONFIGVERSION_FILENAME}"
#        DESTINATION ${CLOG_CONFIG_DESTINATION})

install(TARGETS ${CLOG_TARGET_NAME} DESTINATION lib EXPORT ${CLOG_TARGET_NAME})
install(EXPORT ${CLOG_TARGET_NAME} DESTINATION lib/myproj)


#cmake_minimum_required(VERSION 3.6)
#project(CLog)
#
#add_library(${PROJECT_NAME} INTERFACE)
#include_directories(include)
#target_include_directories(${PROJECT_NAME} INTERFACE
#        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
#        $<INSTALL_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>)
#
#export(TARGETS ${PROJECT_NAME}
#        FILE "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Targets.cmake")
#export(PACKAGE ${PROJECT_NAME})
#
#install(FILES "include/Logger.hpp" DESTINATION include/${PROJECT_NAME})
#install(EXPORT ${PROJECT_NAME}
#        FILE "${PROJECT_NAME}Targets.cmake"
#        DESTINATION cmake)