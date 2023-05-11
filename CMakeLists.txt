cmake_minimum_required(VERSION 3.10)

set(CMAKE_CXX_FLAGS "-g -Wall")
set(CMAKE_CXX_STANDARD 17)

project(VULKANLEARNING)

add_custom_target(
                build_shader
                ALL
                WORKING_DIRECTORY "${PROJECT_SOURCE_DIR}"
                COMMAND glslc "shaders/shader.vert" -o "shaders/vert.spv"
                COMMAND glslc "shaders/shader.frag" -o "shaders/frag.spv")

add_executable(main.out main.cpp)

target_compile_definitions(main.out PUBLIC CURRENT_DIR="${PROJECT_SOURCE_DIR}/")
target_link_libraries(main.out -lglfw -lvulkan)