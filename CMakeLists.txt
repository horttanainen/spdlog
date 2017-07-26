#
# Copyright(c) 2015 Ruslan Baratov.
# Distributed under the MIT License (http://opensource.org/licenses/MIT)
#

cmake_minimum_required(VERSION 3.1)
project(spdlog VERSION 1.0.0)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU" OR "${CMAKE_CXX_COMPILER_ID}" MATCHES "Clang")
    set(CMAKE_CXX_FLAGS "-Wall ${CMAKE_CXX_FLAGS}")
endif()

add_library(spdlog INTERFACE)

option(SPDLOG_BUILD_EXAMPLES "Build examples" OFF)
option(SPDLOG_BUILD_TESTING "Build spdlog tests" ON)

target_include_directories(
    spdlog
    INTERFACE
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/include>"
    "$<INSTALL_INTERFACE:include>"
)

set(HEADER_BASE "${CMAKE_CURRENT_SOURCE_DIR}/include")

if(SPDLOG_BUILD_EXAMPLES)
    add_subdirectory(example)
endif()

if(SPDLOG_BUILD_TESTING)
    add_subdirectory(tests)
endif()

