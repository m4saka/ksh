cmake_minimum_required(VERSION 3.8)
project(ksh CXX)
file(GLOB_RECURSE sources src/*.cpp)
add_library(ksh STATIC ${sources})
if(MSVC)
    if("${CMAKE_BUILD_TYPE}" MATCHES "Debug")
        target_compile_options(ksh PUBLIC /MTd /W4)
        message("Build type: Debug")
    else()
        target_compile_options(ksh PUBLIC /MT /Ox /W4 /DNDEBUG)
        message("Build type: Release")
    endif()
else()
    target_compile_options(ksh PUBLIC -O2 -Wall -fPIC)
endif()
target_compile_features(ksh PUBLIC cxx_std_17)
target_include_directories(ksh PUBLIC ${PROJECT_SOURCE_DIR}/include)
