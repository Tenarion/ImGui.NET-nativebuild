cmake_minimum_required(VERSION 3.1)
Project(cimgui)


set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
#general settings
include_directories(cimgui/imgui)
include_directories(cimplot/implot)
include_directories(cimguizmo/ImGuizmo)
include_directories(cimnodes/imnodes)
#add_definitions("-DIMGUI_DISABLE_OBSOLETE_FUNCTIONS=1")
target_compile_definitions(cimgui PUBLIC IMGUI_DISABLE_OBSOLETE_FUNCTIONS=1)
#add_compile_definitions("IMGUI_DEFINE_MATH_OPERATORS=1")

include_directories(cimgui)
set(IMGUI_SOURCES ./cimgui/cimgui.cpp 
./cimgui/imgui/imgui.cpp 
./cimgui/imgui/imgui_draw.cpp 
./cimgui/imgui/imgui_demo.cpp 
./cimgui/imgui/imgui_widgets.cpp 
./cimplot/cimplot.cpp 
./cimplot/implot/implot.cpp
./cimplot/implot/implot_items.cpp  
./cimplot/implot/implot_demo.cpp
./cimguizmo/cimguizmo.cpp
./cimguizmo/ImGuizmo/ImGuizmo.cpp
)

set(IMGUI_LIBRARIES )

if (WIN32)
    add_definitions("-DIMGUI_IMPL_API=extern \"C\" __declspec\(dllexport\)")
else(WIN32)
    add_definitions("-DIMGUI_IMPL_API=extern \"C\" ")
endif(WIN32)

add_library(cimgui_base OBJECT ${IMGUI_SOURCES})

if(UNIX)
set_property(TARGET cimgui_base PROPERTY POSITION_INDEPENDENT_CODE ON)
endif(UNIX)


#install

install(DIRECTORY lua/imgui DESTINATION ${LUAJIT_BIN}/lua)
