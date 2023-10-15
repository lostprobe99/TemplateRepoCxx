cmake_minimum_required(VERSION 3.20.0)

project(my_project_name VERSION 0.0.1 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
# set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_C_STANDARD 11)

if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
    message("Setting default build type to Release")
endif()

if(MSVC)
    # 为 msvc 指定源文件为 utf8
    add_compile_options("$<$<C_COMPILER_ID:MSVC>:/source-charset:utf-8>")
endif()

message("Current cxx compiler is ${CMAKE_CXX_COMPILER_ID}")
message("Current c compiler is ${CMAKE_C_COMPILER_ID}")

set(C_COMPILER_MACRO IS_${CMAKE_C_COMPILER_ID}_C)
message("C_COMPILER_MACRO is defined ${C_COMPILER_MACRO}")
add_definitions(-D${C_COMPILER_MACRO})

set(CXX_COMPILER_MACRO IS_${CMAKE_CXX_COMPILER_ID}_CXX)
message("CXX_COMPILER_MACRO is defined ${CXX_COMPILER_MACRO}")
add_definitions(-D${CXX_COMPILER_MACRO})

message("Configuring on/for ${CMAKE_SYSTEM_NAME}")
string(TOUPPER ${CMAKE_SYSTEM_NAME} SYSTEM_NAME_UPPER)
set(SYSTEM_MACRO IS_${SYSTEM_NAME_UPPER})
message("SYSTEM_MACRO is defined ${SYSTEM_MACRO}")
add_definitions(-D${SYSTEM_MACRO})

include_directories(${PROJECT_SOURCE_DIR}/include)

add_subdirectory(./src)

add_subdirectory(./test)

add_subdirectory(./example)
