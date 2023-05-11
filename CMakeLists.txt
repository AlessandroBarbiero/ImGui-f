# Example usage:
#  mkdir build
#  cd build
#  cmake -g "Visual Studio 14 2015" ..

cmake_minimum_required(VERSION 3.5)
project(imgui_framework CXX)

set(CMAKE_CXX_STANDARD 14)

# GLFW
set(GLFW_DIR D:\\lib\\glfw\\glfw-3.3.8) # Set this to point to an up-to-date GLFW repo
option(GLFW_BUILD_EXAMPLES "Build the GLFW example programs" OFF)
option(GLFW_BUILD_TESTS "Build the GLFW test programs" OFF)
option(GLFW_BUILD_DOCS "Build the GLFW documentation" OFF)
option(GLFW_INSTALL "Generate installation target" OFF)
option(GLFW_DOCUMENT_INTERNALS "Include internals in documentation" OFF)
add_subdirectory(${GLFW_DIR} binary_dir EXCLUDE_FROM_ALL)
include_directories(${GLFW_DIR}/include)

# Dear ImGui
set(IMGUI_DIR ../ImGUI/)
include_directories(${IMGUI_DIR} ${IMGUI_DIR}/backends ..)

# ImGui Framework
include_directories(src)

# Libraries
find_package(Vulkan REQUIRED)
#find_library(VULKAN_LIBRARY
  #NAMES vulkan vulkan-1)
#set(LIBRARIES "glfw;${VULKAN_LIBRARY}")
set(LIBRARIES "glfw;Vulkan::Vulkan")

# Use vulkan headers from glfw:
include_directories(${GLFW_DIR}/deps)

file(GLOB sources 
    *.cpp
    src/*.hpp
    )

add_executable(example ${sources})
target_link_libraries(example ${LIBRARIES})
target_compile_definitions(example PUBLIC -DImTextureID=ImU64)
