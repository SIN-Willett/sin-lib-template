cmake_minimum_required(VERSION 3.13.4)
project(library-name)

set(CMAKE_C_STANDARD 99)
set(CMAKE_CXX_STANDARD 17)

add_library(library-name)

target_include_directories(library-name PUBLIC inc)
target_sources(library-name PUBLIC
        inc/lib.h src/lib.c
        )

#target_link_libraries(library-name PRIVATE pthread)

add_executable(library-test test/test.cpp)
target_link_libraries(library-test PUBLIC library-name)
target_include_directories(library-test PRIVATE inc)

enable_testing()
add_test(libWorks library-test)
