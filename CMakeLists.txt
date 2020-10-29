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

add_library( range-v3-adapter INTERFACE )
target_include_directories( range-v3-adapter
    INTERFACE src/include )
target_compile_options( range-v3-adapter INTERFACE
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
