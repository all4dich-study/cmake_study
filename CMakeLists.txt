dmake_minimum_required (VERSION 2.6)
project (Tutorial)

# Should we use our own math functions?

option (USE_MYMATH "Use tutorial provided math implementation" ON)

# The Version numbver
set (Tutorial_VERSION_MAJOR 1)
set (Tutorial_VERSION_MINOR 0)
set (Psd ${PROJECT_SOURCE_DIR})
set (Pbd ${PROJECT_BINARY_DIR})

# Configure a header file to pass some of the CMake settings to the source code
configure_file (
    "${PROJECT_SOURCE_DIR}/TutorialConfig.h.in"
    "${PROJECT_SOURCE_DIR}/TutorialConfig.h"	
)

# Add the binary tree to the search path for include files
# so that we will find TutorialConfig.h 
include_directories("${PROJECT_BINARY_DIR}")

add_library(MathFunctions mysqrt.cxx)
include_directories


# Add the Mathfunctions library
if (USE_MYMATH)
    include_directories ("${PROJECT_SOURCE_DIR}/MathFunctions")
    add_subdirectory ("MathFunctions")
    set (EXTRA_LIBS ${EXTRA_LIBS} MathFunctions)
endif

# Add the executable
add_executable(Tutorial tutorial.cxx)
target_link_libraries(Tutorial ${EXTRA_LIBS})
