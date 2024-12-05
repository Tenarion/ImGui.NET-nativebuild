cmake_minimum_required(VERSION 3.4)

project(cimgui)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_BUILD_TYPE "RelWithDebInfo")

if(CMAKE_CXX_COMPILER_ID MATCHES "GNU")
  set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -g")
endif()

if(MSVC)
  set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /Zi")
  set(CMAKE_EXE_LINKER_FLAGS_RELEASE "${CMAKE_EXE_LINKER_FLAGS_RELEASE} /DEBUG /OPT:REF /OPT:ICF")
  set(CMAKE_SHARED_LINKER_FLAGS_RELEASE "${CMAKE_SHARED_LINKER_FLAGS_RELEASE} /DEBUG /OPT:REF /OPT:ICF")
endif()


add_library(cimgui SHARED 
    cimgui/cimgui.cpp
    cimgui/imgui/imgui.cpp
    cimgui/imgui/imgui_draw.cpp
    cimgui/imgui/imgui_demo.cpp
    cimgui/imgui/imgui_widgets.cpp
	cimgui/imgui/imgui_tables.cpp)

target_compile_definitions(cimgui PUBLIC IMGUI_DEFINE_MATH_OPERATORS=1)
target_compile_definitions(cimgui PUBLIC IMGUI_DISABLE_OBSOLETE_FUNCTIONS=1)
set_target_properties(cimgui PROPERTIES PREFIX "")


add_library(cimplot SHARED
	cimgui
    cimgui/imgui/imgui.cpp
    cimgui/imgui/imgui_draw.cpp
    cimgui/imgui/imgui_demo.cpp
    cimgui/imgui/imgui_widgets.cpp
	cimgui/imgui/imgui_tables.cpp
    cimplot/cimplot.cpp
    cimplot/implot/implot.cpp
    cimplot/implot/implot_demo.cpp
    cimplot/implot/implot_items.cpp)

target_compile_definitions(cimplot PUBLIC IMGUI_DEFINE_MATH_OPERATORS=1)
target_include_directories(cimplot PUBLIC cimgui)
target_include_directories(cimplot PUBLIC cimgui/imgui)
set_target_properties(cimplot PROPERTIES PREFIX "")


add_library(cimnodes SHARED
    cimgui/imgui/imgui.cpp
    cimgui/imgui/imgui_draw.cpp
    cimgui/imgui/imgui_demo.cpp
    cimgui/imgui/imgui_widgets.cpp
	cimgui/imgui/imgui_tables.cpp
    cimnodes/cimnodes.cpp
    cimnodes/imnodes/imnodes.cpp)

target_compile_definitions(cimnodes PUBLIC IMGUI_DEFINE_MATH_OPERATORS=1)
target_compile_definitions(cimnodes PUBLIC IMNODES_NAMESPACE=imnodes)
target_include_directories(cimnodes PUBLIC cimgui)
target_include_directories(cimnodes PUBLIC cimgui/imgui)
set_target_properties(cimnodes PROPERTIES PREFIX "")


add_library(cimguizmo SHARED
    cimgui/imgui/imgui.cpp
    cimgui/imgui/imgui_draw.cpp
    cimgui/imgui/imgui_demo.cpp
    cimgui/imgui/imgui_widgets.cpp
	cimgui/imgui/imgui_tables.cpp
    cimguizmo/cimguizmo.cpp
    cimguizmo/ImGuizmo/ImGuizmo.cpp)

target_compile_definitions(cimguizmo PUBLIC IMGUI_DEFINE_MATH_OPERATORS=1)
target_include_directories(cimguizmo PUBLIC cimgui)
target_include_directories(cimguizmo PUBLIC cimgui/imgui)
set_target_properties(cimguizmo PROPERTIES PREFIX "")