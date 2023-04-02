cmake_minimum_required(VERSION 3.20)
Project(cimgui)
if(WIN32) #to mingw work as all the others
set(CMAKE_SHARED_LIBRARY_PREFIX "")
endif(WIN32)
#general settings
include_directories(cimgui/imgui)
include_directories(cimplot/implot)
include_directories(cimguizmo/ImGuizmo)
include_directories(cimnodes/imnodes)
add_definitions("-DIMGUI_DISABLE_OBSOLETE_FUNCTIONS=1")

add_compile_definitions("IMGUI_DEFINE_MATH_OPERATORS=1")

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
./cimnodes/cimnodes.cpp
./cimnodes/imnodes/imnodes.cpp
)

if (EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/cimgui/imgui/backends)
	set(BAKENDS_FOLDER "./cimgui/imgui/backends/")
else()
	set(BAKENDS_FOLDER "./cimgui/imgui/examples/")
endif()

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
