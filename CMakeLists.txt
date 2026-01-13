cmake_minimum_required(VERSION 3.21)

project(VulkanTriangle LANGUAGES CXX)

# C++ standard (required by Vulkan tutorial)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Prefer clang
set(CMAKE_C_COMPILER clang)
set(CMAKE_CXX_COMPILER clang++)

# Find Vulkan (from Vulkan SDK)
find_package(Vulkan REQUIRED)

# Add GLFW submodule
# Assumes: external/glfw contains the GLFW repo
add_subdirectory(external/glfw)

# Build executable
add_executable(VulkanTriangle
    main.cpp
)

# Link libraries
target_link_libraries(VulkanTriangle PRIVATE
    Vulkan::Vulkan
    glfw
)

# Platform-specific notes:
# - On Windows, GLFW automatically links win32, user32, gdi32, etc.
# - On Linux, X11/Wayland deps are handled by GLFW's CMake
# - On macOS, Cocoa frameworks are handled automatically
