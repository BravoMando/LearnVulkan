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

if(MSVC)
    target_link_directories(main.out PRIVATE E:/VSCODE/github/Utils/glfw-3.3.8.bin.WIN64/glfw-3.3.8.bin.WIN64/lib-vc2022)
elseif(MINGW)
    target_link_directories(main.out PRIVATE E:/VSCODE/github/Utils/glfw-3.3.8.bin.WIN64/glfw-3.3.8.bin.WIN64/lib-mingw-w64)
endif()

target_include_directories(main.out PRIVATE E:/VSCODE/github/Utils/glfw-3.3.8.bin.WIN64/glfw-3.3.8.bin.WIN64/include)
target_include_directories(main.out PRIVATE $ENV{VULKAN_SDK}/Include)
target_include_directories(main.out PRIVATE E:/VSCODE/github/Utils/glm)
target_link_directories(main.out PRIVATE $ENV{VULKAN_SDK}/Lib)
target_link_libraries(main.out PRIVATE glfw3 vulkan-1)
