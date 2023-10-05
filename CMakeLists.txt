# CMakeList.txt : CMake project for cmake-simple, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

project ("ffmpeg-examples")

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

set(LIBRARIES_FOR_LINK
    PkgConfig::LIBAV
    m
)

find_package(PkgConfig REQUIRED)
pkg_check_modules(LIBAV REQUIRED IMPORTED_TARGET
    libavdevice
    libavfilter
    libavformat
    libavcodec
    libswresample
    libswscale
    libavutil
)

# Add source to this project's executable.
add_executable (cmake-simple "cmake-simple.cpp" "cmake-simple.h")
add_executable (decode_audio "decode_audio.c")

# NOTE: 'm' means linking with the math library (libm)
target_link_libraries(decode_audio PRIVATE ${LIBRARIES_FOR_LINK})
