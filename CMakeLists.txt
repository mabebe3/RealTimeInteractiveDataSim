cmake_minimum_required(VERSION 3.21)
project(RealTimeInteractiveDataSim LANGUAGES CXX CUDA)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(CMAKE_PREFIX_PATH "${CMAKE_SOURCE_DIR}/vcpkg_installed/x64-windows")

find_package(glfw3 CONFIG REQUIRED)
find_package(imgui CONFIG REQUIRED)
find_package(implot CONFIG REQUIRED)
find_package(Arrow CONFIG REQUIRED)
find_package(TBB CONFIG REQUIRED)
find_package(Boost REQUIRED COMPONENTS signals2)

enable_language(CUDA)

add_executable(RTIDViz
    src/main.cpp
    src/backends/imgui_impl_glfw.cpp
    src/backends/imgui_impl_opengl3.cpp
)

target_include_directories(RTIDViz PRIVATE include)

target_link_libraries(RTIDViz PRIVATE
    glfw3
    imgui::imgui
    implot::implot
    Arrow::arrow_shared
    TBB::tbb
    Boost::signals2
)