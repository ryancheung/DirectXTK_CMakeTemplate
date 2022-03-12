cmake_minimum_required (VERSION 3.11)

project ("Client")

option(ENABLE_CODE_ANALYSIS "Use Static Code Analysis on build" OFF)

SET(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")

if(CMAKE_SIZEOF_VOID_P EQUAL 8)
  # 64 bits
elseif(CMAKE_SIZEOF_VOID_P EQUAL 4)
  # 32 bits
endif()

# set macro-directory
list(APPEND CMAKE_MODULE_PATH
  "${CMAKE_SOURCE_DIR}/cmake/macros")

if(CMAKE_VERSION VERSION_LESS "3.16.0")
  list(APPEND CMAKE_MODULE_PATH
    "${CMAKE_SOURCE_DIR}/dep/cotire/CMake")
endif()

include(AutoCollect)

find_package(PCHSupport)
find_package(directxtk CONFIG REQUIRED)

add_subdirectory(src)
