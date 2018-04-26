cmake_minimum_required(VERSION 2.8.7)

set(PROJECT_NAME_STR example_lib_gatb)
project(${PROJECT_NAME_STR} C CXX)

find_package(Threads REQUIRED)
find_package(ZLIB REQUIRED)

include(${PROJECT_SOURCE_DIR}/ext/gatb.cmake)

link_directories(${CMAKE_BINARY_DIR}/lib)
set(EXTERNAL_LIBS
        gatbcore
        hdf5
        hdf5_tools)

add_executable(${PROJECT_NAME} ${PROJECT_SOURCE_DIR}/src/main.cpp)
add_dependencies(${PROJECT_NAME} gatb)
target_link_libraries(${PROJECT_NAME}
        ${CMAKE_THREAD_LIBS_INIT}
        ${EXTERNAL_LIBS}
        ${CMAKE_DL_LIBS}
        ${ZLIB_LIBRARY})
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_BINARY_DIR}/include)
