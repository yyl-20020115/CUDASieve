cmake_minimum_required(VERSION 3.26)
project(CUDASieve CXX CUDA)
set(CUDASieve_VERSION "12.4")
set(CUDASieve_SOVERSION "12.4.0")


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

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

set(CMAKE_INSTALL_INCLUDEDIR "${CMAKE_INSTALL_PREFIX}/include/CUDASieve")
# Install headers ####################################################

install(FILES 
              include/CUDASieve/cstest.hpp
              include/CUDASieve/cudasieve.hpp
              include/CUDASieve/device.cuh
              include/CUDASieve/global.cuh
              include/CUDASieve/host.hpp
              include/CUDASieve/launch.cuh
              include/CUDASieve/primelist.cuh
              include/CUDASieve/primeoutlist.cuh
              COMPONENT CUDASieveHeaders
              DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})


# CMake find_package(CUDASieve) support #############################

write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/CUDASieveConfigVersion.cmake"
    VERSION ${CUDASieve_VERSION}
    COMPATIBILITY SameMajorVersion)

configure_package_config_file(
    "${PROJECT_SOURCE_DIR}/cmake/CUDASieveConfig.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/CUDASieveConfig.cmake"
    PATH_VARS CMAKE_INSTALL_PREFIX
    INSTALL_DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/CUDASieve")

install(FILES "${CMAKE_CURRENT_BINARY_DIR}/CUDASieveConfig.cmake"
              "${CMAKE_CURRENT_BINARY_DIR}/CUDASieveConfigVersion.cmake"
        DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/CUDASieve")

install(TARGETS CUDASieve
        EXPORT CUDASieve
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR})