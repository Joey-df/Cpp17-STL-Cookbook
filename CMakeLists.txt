cmake_minimum_required(VERSION 3.27)
project(Cpp17_STL_Cookbook)


set(CMAKE_CXX_STANDARD 17)
# 查找并加载外部库fmt
find_package(fmt)

# get source files
file(GLOB_RECURSE sources RELATIVE ${PROJECT_SOURCE_DIR} "*.cpp")

# add the binary tree to the search path for include files
include_directories("${PROJECT_SOURCE_DIR}")

# set output path
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

# add the executable
foreach(file ${sources})
    string(REPLACE "/" "_" target_name ${file})
    # message(${file} \ \ \ \ \ ${target_name})
    string(REPLACE ".cpp" "" target_name ${target_name})
    add_executable (${target_name} ${file})
    # link fmt libraries
    target_link_libraries(${target_name} fmt::fmt)
    message ("  -- src/${file} will be compiled to bin/${target_name}")
endforeach()
