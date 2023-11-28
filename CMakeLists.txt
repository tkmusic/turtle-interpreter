cmake_minimum_required(VERSION 3.10)
project(Turtle C)

# Set the C standard to C11
set(CMAKE_C_STANDARD 11)

# Source files
set(SOURCES
    src/main.c
    # Add more source files as needed
)

# Create the executable
add_executable(turtle ${SOURCES})

# Set the output directory for the executable
set_target_properties(turtle PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/build
)

# You can add additional compiler flags if needed
# For example, to enable warnings, you can use:
# target_compile_options(turtle PRIVATE -Wall -Wextra)

# You can add additional include directories if needed
# For example, to include a 'include' directory, you can use:
# target_include_directories(turtle PRIVATE include)
