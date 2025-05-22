# Raylib_CMake_Setup
To help install any raylib version in any computer that supports CMake.

Remember to take a look at the "CMakeLists.txt" file. You may need to modify it based on your needs.

If you create a dir called "src" and put your source files (".c") inside, they will be automaticaly recognized by the compiler.

In the same way, if you create a dir called "inc" and put your header files (".h") inside, they will be automaticaly reconized by the compiler 

When you compile the project all the binaries generated will be inside the "bin" directory.

# Dependencies
You will need some dependencies:
    * CMake - at least version 3.24
    * A C/C++ compiler 

# How to compile a project
Follow this steps
    1. create the CMakeCache.txt file in the build folder
    for this we will use 2 commands
    
    `cd build `
    
    and then 

    `cmake ..`

    the cmake will try to create the cache file

    after creating it go back to the main directory of the project using the command

    `cd ..`

    2. Compile the project using this command
    
    `cmake --build build`

For the rest of the project assuming you did everthing correct for compiling any amount of times you will only nedd the second command



