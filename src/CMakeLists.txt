include_directories("${CMAKE_SOURCE_DIR}/src")
add_subdirectory(CUDASieve)
add_executable(CUDASieveMain main.cpp)
target_link_libraries(CUDASieveMain CUDASieve)


option(ENABLE_TESTS OFF "Enable tests")
if(${ENABLE_TESTS})
find_package(boost REQUIRED)
find_package(primesieve REQUIRED)

include_directories(${Boost_INCLUDE_DIRS})

add_executable(CUDASieveTest cstest.cpp)
target_link_libraries(CUDASieveTest CUDASieve ${Boost_LIBRARIES} primesieve::libprimesieve)
endif(${ENABLE_TESTS})
