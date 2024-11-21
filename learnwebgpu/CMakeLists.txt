# CMakeList.txt : CMake project for learnwebgpu, include source and define
# project specific logic here.
#

# Add source to this project's executable.

find_package(Dawn REQUIRED)
add_executable (learnwebgpu "learnwebgpu.cpp" "learnwebgpu.h")

cmake_minimum_required(VERSION 3.0...3.25)
project(
    LearnWebGPU # name of the project, which will also be the name of the visual studio solution if you use it
    VERSION 0.1.0 # any version number
    LANGUAGES CXX C # programming languages used by the project
)

set_target_properties(learnwebgpu PROPERTIES
    CXX_STANDARD 23
    CXX_STANDARD_REQUIRED ON
    CXX_EXTENSIONS OFF
    COMPILE_WARNING_AS_ERROR ON
)

if (MSVC)
    target_compile_options(learnwebgpu PRIVATE /W4)
else()
    target_compile_options(learnwebgpu PRIVATE -Wall -Wextra -pedantic)
endif()

if (XCODE)
    set_target_properties(App PROPERTIES
        XCODE_GENERATE_SCHEME ON
        XCODE_SCHEME_ENABLE_GPU_FRAME_CAPTURE_MODE "Metal"
    )
endif()

target_link_libraries(learnwebgpu dawn::webgpu_dawn)
# TODO: Add tests and install targets if needed.
