########################################################################
# Preamble
########################################################################

cmake_minimum_required( VERSION 3.14 )
project( range-v3-adapter LANGUAGES CXX )


########################################################################
# Project-wide setup
########################################################################

set( CMAKE_CXX_STANDARD 17 )
set( CMAKE_CXX_STANDARD_REQUIRED YES )

option( range-v3-adapter_unit_tests
    "Compile the range-v3-adapter unit tests and integrate with ctest" ON
    )
option( strict_compile
    "Treat all warnings as errors." ON
    )

# Compile flags
set( common_flags "-Wall" "-Wextra" "-Wpedantic" )
set( strict_flags "-Werror" )
set( release_flags "-O3" )
set( debug_flags "-O0" "-g" )


########################################################################
# Project targets
########################################################################

add_library( range-v3-adapter 
    src/cmake/aligned_new_probe.cpp
    src/cmake/coro_test_code.cpp
    src/example/any_all_none_of.cpp
    src/example/calendar.cpp
    src/example/comprehensions.cpp
    src/example/count.cpp
    src/example/count_if.cpp
    src/example/fibonacci.cpp
    src/example/find.cpp
    src/example/for_each_assoc.cpp
    src/example/for_each_sequence.cpp
    src/example/hello.cpp
    src/example/is_sorted.cpp
    src/perf/counted_insertion_sort.cpp
    src/perf/sort_patterns.cpp
    src/test_package/example.cpp
    )
target_include_directories( range-v3-adapter PUBLIC src/ )
target_compile_options( range-v3-adapter PRIVATE
    ${common_flags}
    $<$<BOOL:${strict_compile}>:${strict_flags}>
    $<$<CONFIG:DEBUG>:${debug_flags}>
    $<$<CONFIG:RELEASE>:${release_flags}>
    )


#######################################################################
# Top-level Only
#######################################################################

if( CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR )

    # unit testing
    if( range-v3-adapter_unit_tests )
        include( cmake/unit_testing.cmake )
    endif()

endif()
