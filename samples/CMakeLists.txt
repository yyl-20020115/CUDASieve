
add_executable(benchmark benchmark.cu)
target_link_libraries(benchmark CUDASieve)
add_executable(sumPrimes sumPrimes.cu)
target_link_libraries(sumPrimes CUDASieve)
