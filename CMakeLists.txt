cmake_minimum_required(VERSION 3.10)
set(PROJECT_NAME SFML-media-demo)
project(${PROJECT_NAME})

set(CMAKE_CXX_STANDARD 11)

if (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
elseif(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -static")
endif (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")


set(SOURCE_FILES main.cpp)
add_executable(${PROJECT_NAME} ${SOURCE_FILES})

if (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
elseif(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
else()
    set(SFML_STATIC_LIBRARIES TRUE)
endif (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake_modules")

find_package(SFML REQUIRED system window graphics network audio)
if (SFML_FOUND)
    include_directories(${SFML_INCLUDE_DIR} ${PROJECT_SOURCE_DIR})
    target_link_libraries(${PROJECT_NAME} ${SFML_LIBRARIES})
endif()