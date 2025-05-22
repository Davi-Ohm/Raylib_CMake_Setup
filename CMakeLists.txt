# set the minimal cmake version
cmake_minimum_required(VERSION 3.24)

# set the name of the project
project(SlowRacer C)

# set the c standart
set(CMAKE_C_STANDARD 23)

#test
set(CMAKE_POLICY_VERSION_MINIMUM 3.5)

# checks if the program recived any instructions about the optimization during the build process 
# if not set the mode to "debug" wich implies in the optimization level of "-O1" or not optimized
if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)

    message(
        STATUS "No build type especified, defaulting to Debug mode"
    )

    set(
        CMAKE_BUILD_TYPE "Debug" 
        CACHE STRING "Chose the type"
    )
    
endif()

message(STATUS "Build type: ${CMAKE_BUILD_TYPE}")

# Output dir
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

# Include the raylib direct from github
include(FetchContent)

# Set the version of the raylib that will be used
set(RAYLIB_VERSION 5.5)

FetchContent_Declare(
    raylib
    URL https://github.com/raysan5/raylib/archive/refs/tags/${RAYLIB_VERSION}.tar.gz
)

# this desables the raylib compiling of raylib examples
set(BUILD_EXAMPLES OFF CACHE INTERNAL "")

FetchContent_MakeAvailable(raylib)

# Get all source ".c" files from project folders
file(
    GLOB_RECURSE SOURCE_FILES
    ${CMAKE_SOURCE_DIR}/src/*.c
    ${CMAKE_SOURCE_DIR}/libs/src/*.c
)


# tell what is the "main" file to the project
add_executable(
    ${PROJECT_NAME} ${SOURCE_FILES}
)

# Add include directories
target_include_directories(
    ${PROJECT_NAME} PRIVATE
    ${CMAKE_SOURCE_DIR}/inc
    ${CMAKE_SOURCE_DIR}/libs/inc
)

# Link with raylib
# the "PRIVATE" aspect makes so the raylib is not automaticaly passed to 
# other projetcs that include my project "SlowRacer" in this case
target_link_libraries(SlowRacer raylib)


# Checks if OSX and links appropriate frameworks (Only required on MacOS)
if (APPLE)
    target_link_libraries(${PROJECT_NAME} "-framework IOKit")
    target_link_libraries(${PROJECT_NAME} "-framework Cocoa")
    target_link_libraries(${PROJECT_NAME} "-framework OpenGL")
endif()

# Isso esta incompleto mas está um bom incompleto 
# Feito por Davi Santos - 2025