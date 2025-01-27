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

file(GLOB CIMGUI_SOURCES
    "cimgui/*.cpp"
    "cimgui/imgui/*.cpp"
    "cimplot/*.cpp"
    "cimplot/implot/*.cpp"
    "cimnodes/*.cpp"
    "cimnodes/imnodes/*.cpp"
    "cimguizmo/*.cpp"
    "cimguizmo/ImGuizmo/*.cpp"
    "cimguiextra/cimgui_extra/*.cpp"
    "cimguiextra/extra/*.cpp"
    "cimguiextra/cimgui_knobs/*.cpp"
    "cimguiextra/imgui-knobs/*.cpp"
    "cimguiextra/cimgui_notify/*.cpp"
    "cimguiextra/imgui_notify/*.cpp"
    "cimguiextra/cimgui_theme/*.cpp"
    "cimguiextra/imgui_theme/*.cpp"
)

add_library(cimgui SHARED ${CIMGUI_SOURCES})

target_compile_definitions(cimgui 
    PUBLIC 
        IMGUI_DEFINE_MATH_OPERATORS=1
	    IMNODES_NAMESPACE=imnodes
        IMGUI_DISABLE_OBSOLETE_FUNCTIONS=1
)
target_include_directories(cimgui PUBLIC cimgui)
target_include_directories(cimgui PUBLIC cimgui/imgui)
target_include_directories(cimgui PUBLIC cimplot)
target_include_directories(cimgui PUBLIC cimnodes)
target_include_directories(cimgui PUBLIC cimguizmo)
target_include_directories(cimgui PUBLIC cimguiextra)
set_target_properties(cimgui PROPERTIES PREFIX "")
