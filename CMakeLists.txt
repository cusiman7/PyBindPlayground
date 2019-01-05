cmake_minimum_required (VERSION 3.10)
project (PyBindPlayground)

find_package(SDL2 REQUIRED)
find_package(OpenGL REQUIRED)
find_package(pybind11 REQUIRED)
find_library(COCOA Cocoa)

add_library(imgui
    third_party/imgui/imgui.h
    third_party/imgui/imgui.cpp
    third_party/imgui/imgui_demo.cpp
    third_party/imgui/imgui_draw.cpp
    third_party/imgui/imgui_widgets.cpp
    third_party/imgui/examples/imgui_impl_opengl3.h
    third_party/imgui/examples/imgui_impl_opengl3.cpp
    third_party/imgui/examples/imgui_impl_sdl.h
    third_party/imgui/examples/imgui_impl_sdl.cpp
    third_party/imgui/examples/libs/gl3w/GL/gl3w.c
    third_party/imgui/examples/libs/gl3w/GL/gl3w.h
    third_party/imgui/examples/libs/gl3w/GL/glcorearb.h
) 
target_include_directories(imgui PUBLIC
    third_party/imgui
    third_party/imgui/examples
    third_party/imgui/examples/libs/gl3w
    ${SDL2_INCLUDE_DIRS}
)
target_link_libraries(imgui
    PUBLIC
    ${SDL2_LIBRARIES}
    ${OpenGL_LIBRARIES}
    ${COCOA}
)

add_executable(PyBindPlayground 
    src/main.cpp
)
target_link_libraries(PyBindPlayground
    PRIVATE
    imgui
    pybind11::embed
)
target_compile_features(PyBindPlayground
    PUBLIC
    cxx_std_17
)

