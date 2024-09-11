cmake_minimum_required(VERSION 3.26)
project(CUDASieve CXX CUDA)

set(CMAKE_CXX_STANDARD 17)
set(CUDA_ARCHITECTURES 70 75 80 86)

find_package(CUDA REQUIRED)
find_package(OpenMP REQUIRED)
find_package(Threads REQUIRED)

set(CMAKE_CUDA_STANDARD 17)
set(CMAKE_CUDA_STANDARD_REQUIRED ON)
set(CMAKE_CUDA_EXTENSIONS OFF)

include_directories("${CMAKE_SOURCE_DIR}/include")

add_subdirectory(src)
add_subdirectory(samples)
