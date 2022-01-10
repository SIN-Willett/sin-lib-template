cmake_minimum_required(VERSION 3.13.4)
project(library-test VERSION 0.1)

find_package(library-name REQUIRED)

set(CMAKE_C_STANDARD 99)
set(CMAKE_CXX_STANDARD 17)

add_executable(library-test test.cpp)
target_link_libraries(library-test PUBLIC library-name::library-name)

enable_testing()
add_test(libWorks library-test)