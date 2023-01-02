cmake_minimum_required(VERSION 3.10)

#set the project name and version
project(Tutorial VERSION 1.0)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 11)            # Use C++11
set(CMAKE_CXX_STANDARD_REQUIRED True) # No really, I mean it

# add the executable
add_executable(Tutorial tutorial.cxx)
configure_file(TutorialConfig.h.in TutorialConfig.h)
target_include_directories(Tutorial PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           )