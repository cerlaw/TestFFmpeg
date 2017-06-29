# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)
set(lib_src_DIR ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI})

add_library(native-lib  SHARED src/main/cpp/native-lib.cpp)
add_library(avcodec-57 SHARED IMPORTED)
add_library(avformat-57 SHARED IMPORTED)
add_library(avutil-55 SHARED IMPORTED)
add_library(swresample-2 SHARED IMPORTED)
add_library(swscale-4 SHARED IMPORTED)

set_target_properties(avcodec-57 PROPERTIES IMPORTED_LOCATION
${lib_src_DIR}/libavcodec-57.so)
set_target_properties(avformat-57 PROPERTIES IMPORTED_LOCATION
${lib_src_DIR}/libavformat-57.so)
set_target_properties(avutil-55 PROPERTIES IMPORTED_LOCATION
${lib_src_DIR}/libavutil-55.so)
set_target_properties(swresample-2 PROPERTIES IMPORTED_LOCATION
${lib_src_DIR}/libswresample-2.so)
set_target_properties(swscale-4 PROPERTIES IMPORTED_LOCATION
${lib_src_DIR}/libswscale-4.so)

include_directories(${CMAKE_SOURCE_DIR}/src/main/cpp/include)

find_library(log-lib log )
target_link_libraries(  native-lib ${log-lib} avcodec-57
avformat-57
avutil-55
swresample-2
swscale-4)