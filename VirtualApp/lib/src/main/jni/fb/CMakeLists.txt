
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_C_STANDARD 11)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DLOG_TAG=\"libfb\" -DDISABLE_CPUCAP -DDISABLE_XPLAT -fexceptions -frtti")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Werror")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-unused-parameter")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DHAVE_POSIX_CLOCKS")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=gnu++11")

add_library(fb STATIC
    assert.cpp
    jni/ByteBuffer.cpp
    jni/Countable.cpp
    jni/Environment.cpp
    jni/Exceptions.cpp
    jni/fbjni.cpp
    jni/Hybrid.cpp
    jni/jni_helpers.cpp
    jni/LocalString.cpp
    jni/OnLoad.cpp
    jni/References.cpp
    jni/WeakReference.cpp
    log.cpp
    lyra/lyra.cpp
    onload.cpp
)

add_definitions(-DHAVE_POSIX_CLOCKS)
add_definitions(-DDISABLE_CPUCAP)
add_definitions(-DDISABLE_XPLAT)

target_compile_definitions(fb PRIVATE -DLOG_TAG="libfb")


target_include_directories(fb PRIVATE . include)
target_link_libraries(fb log dl android)