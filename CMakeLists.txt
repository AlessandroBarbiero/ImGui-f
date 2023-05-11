# Example usage:
#  mkdir build
#  cd build
#  cmake -G "Visual Studio 16 2019" ..

cmake_minimum_required(VERSION 3.5)
project(imgui_framework CXX)

set(CMAKE_CXX_STANDARD 14)

# GLFW
set(GLFW_DIR D:\\lib\\glfw\\glfw-3.3.8) # -----> Set this to point to an up-to-date GLFW repo

option(GLFW_BUILD_EXAMPLES "Build the GLFW example programs" OFF)
option(GLFW_BUILD_TESTS "Build the GLFW test programs" OFF)
option(GLFW_BUILD_DOCS "Build the GLFW documentation" OFF)
option(GLFW_INSTALL "Generate installation target" OFF)
option(GLFW_DOCUMENT_INTERNALS "Include internals in documentation" OFF)
add_subdirectory(${GLFW_DIR} binary_dir EXCLUDE_FROM_ALL)
include_directories(${GLFW_DIR}/include)

# Dear ImGui
set(IMGUI_DIR ../ImGUI/)    # -------> Set this to point to an up-to-date Dear ImGui repo

include_directories(${IMGUI_DIR} ${IMGUI_DIR}/backends ..)
file(GLOB imgui_files
    ${IMGUI_DIR}/backends/imgui_impl_glfw.cpp 
    ${IMGUI_DIR}/backends/imgui_impl_vulkan.cpp 
    ${IMGUI_DIR}/imgui.cpp 
    ${IMGUI_DIR}/imgui_draw.cpp 
    ${IMGUI_DIR}/imgui_demo.cpp 
    ${IMGUI_DIR}/imgui_tables.cpp 
    ${IMGUI_DIR}/imgui_widgets.cpp
)

# ImGui Framework
include_directories(src)

# Libraries
find_package(Vulkan REQUIRED)
set(LIBRARIES "glfw;Vulkan::Vulkan")

# Use vulkan headers from glfw:
include_directories(${GLFW_DIR}/deps)

file(GLOB sources 
    *.cpp
    src/*.hpp
    )

add_executable(example ${sources} ${imgui_files})
target_link_libraries(example ${LIBRARIES})
target_compile_definitions(example PUBLIC -DImTextureID=ImU64)