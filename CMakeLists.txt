cmake_minimum_required(VERSION 3.14)

project(storage_charge VERSION 1.0.0 LANGUAGES C CXX)

# global options
option(ENABLE_TEST "enable test for storage charge" ON)

# c++ standard
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# enable warnings
if (CMAKE_CXX_COMPILER_ID MATCHES "Clang" OR CMAKE_CXX_COMPILER_ID MATCHES "GNU")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -pedantic")
endif()

# find external deps
find_package(GTest)

# enable testing
if (ENABLE_TEST)
  include(CTest)
  enable_testing()
endif()

# target: storage_charge
file(GLOB all_srcs CONFIGURE_DEPENDS
  src/*.cc
  src/*.c
)

add_library(storage_charge ${all_srcs})

target_include_directories(storage_charge 
  PUBLIC 
    include
  PRIVATE
    src
)

if(BUILD_TESTING)
  add_subdirectory(test)
endif()