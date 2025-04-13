cmake_minimum_required(VERSION 3.2.0)
project(qhttpengine)

set(PROJECT_NAME "QHttpEngine")
set(PROJECT_DESCRIPTION "Simple and secure HTTP server for Qt applications")
set(PROJECT_AUTHOR "Nathan Osman")
set(PROJECT_URL "https://github.com/nitroshare/qhttpengine")

set(PROJECT_VERSION_MAJOR 1)
set(PROJECT_VERSION_MINOR 0)
set(PROJECT_VERSION_PATCH 1)
set(PROJECT_VERSION ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH})

include(GNUInstallDirs)

# Build a shared library by default
option(BUILD_SHARED_LIBS "Build QHttpEngine as a shared library" ON)

set(DOC_INSTALL_DIR share/doc/qhttpengine CACHE STRING "Documentation installation directory relative to the install prefix")
set(EXAMPLES_INSTALL_DIR "${CMAKE_INSTALL_LIBDIR}/qhttpengine/examples" CACHE STRING "Examples installation directory relative to the install prefix")

find_package(Qt5Network 5.4 REQUIRED)

set(CMAKE_AUTOMOC ON)

add_subdirectory(src)

option(BUILD_DOC "Build Doxygen documentation" OFF)
if(BUILD_DOC)
    find_package(Doxygen REQUIRED)
    add_subdirectory(doc)
endif()

option(BUILD_EXAMPLES "Build the example applications" OFF)
if(BUILD_EXAMPLES)
    add_subdirectory(examples)
endif()

option(BUILD_TESTS "Build the test suite" OFF)
if(BUILD_TESTS)
    find_package(Qt5Test 5.4 REQUIRED)
    enable_testing()
    add_subdirectory(tests)
endif()
