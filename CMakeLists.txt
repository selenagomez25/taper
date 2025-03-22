cmake_minimum_required(VERSION 3.31)
project(taper)

if (POLICY CMP0141)
    cmake_policy(SET CMP0141 NEW)
    cmake_policy(SET CMP0091 NEW)
    set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

set(CMAKE_CXX_STANDARD 20)

add_library(taper SHARED src/main.cpp)

target_include_directories(taper PUBLIC "include/jni")

target_link_directories(taper PUBLIC "lib")
target_link_libraries(taper PUBLIC "jvm")

if(MSVC)
    set_property(TARGET taper PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
endif()

if (CMAKE_VERSION VERSION_GREATER 3.12)
    set_property(TARGET taper PROPERTY CXX_STANDARD 20)
endif()

if(WIN32)
    target_include_directories(taper PUBLIC "include/jni/win32")
endif()