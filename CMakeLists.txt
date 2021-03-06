project(SPRITER_PLUS_PLUS)
cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

if(${PROJECT_BINARY_DIR} STREQUAL ${PROJECT_SOURCE_DIR})
   message(FATAL_ERROR "In-tree build attempt detected, aborting. Set your build dir outside your source dir, delete CMakeCache.txt from source root and try again.")
endif()

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -Wno-sign-compare -Wno-reorder -Wno-unused-variable")

option(SKIP_EXAMPLES "Only build the spriterengine and skip all examples" OFF)

file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/Release/GreyGuy
    ${CMAKE_CURRENT_SOURCE_DIR}/Release/PT-Sans
    DESTINATION ${CMAKE_RUNTIME_OUTPUT_DIRECTORY})

add_subdirectory(spriterengine)

if(NOT SKIP_EXAMPLES)
    add_subdirectory(pugixml)
    add_subdirectory(tinyxml2)
    add_subdirectory(example)
endif(NOT SKIP_EXAMPLES)
