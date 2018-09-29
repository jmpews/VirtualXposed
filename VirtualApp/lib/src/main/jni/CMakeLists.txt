cmake_minimum_required(VERSION 3.4.1)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_C_STANDARD 11)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-error=format-security -fpermissive -DLOG_TAG=\"VA++\" -fno-rtti -fno-exceptions")


include_directories(. ./Foundation ./Jni ./fb/include ./include)

add_library(va++ SHARED
    Jni/VAJni.cpp
    Foundation/IOUniformer.cpp
    Foundation/VMPatch.cpp
    Foundation/SymbolFinder.cpp
    Foundation/Path.cpp
    Foundation/SandboxFs.cpp
    Foundation/fake_dlfcn.cpp
)

target_compile_definitions(va++ PRIVATE -DLOG_TAG="VA++")
add_subdirectory(fb)
target_link_libraries(va++ fb)

target_link_libraries(va++ log atomic fb)


message(STATUS "[*] initialize HookZz")
macro(SET_OPTION option value)
    set(${option} ${value} CACHE INTERNAL "" FORCE)
endmacro()

SET_OPTION(PLATFORM Android)
SET_OPTION(SHARED ON)
SET_OPTION(DEBUG ON)
SET_OPTION(CMAKE_VERBOSE_MAKEFILE ON)
add_subdirectory(HookZz)
target_link_libraries(va++ hookzz)