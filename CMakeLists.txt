cmake_minimum_required(VERSION 2.8.11)
project(test_ordered_map)
enable_testing()

find_package(Boost 1.54.0 REQUIRED COMPONENTS unit_test_framework) 

if(CMAKE_CXX_COMPILER_ID MATCHES "Clang" OR CMAKE_CXX_COMPILER_ID MATCHES "GNU")
    #set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -std=c++11 -Werror -Wall -Wextra -Wold-style-cast -g --coverage -DTSL_DEBUG")
    set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -std=c++11 -Werror -Wall -Wextra -Wold-style-cast -O3 -DTSL_DEBUG")
endif()


set(TEST_EXECUTABLE "test_ordered_map")



add_executable("${TEST_EXECUTABLE}" "tests/main.cpp" "tests/ordered_map_tests.cpp" "tests/ordered_set_tests.cpp")
target_include_directories("${TEST_EXECUTABLE}" PRIVATE "${Boost_INCLUDE_DIRS}" "src") 
target_link_libraries("${TEST_EXECUTABLE}" ${Boost_LIBRARIES})

add_test(NAME "all_tests" COMMAND "${TEST_EXECUTABLE}")
