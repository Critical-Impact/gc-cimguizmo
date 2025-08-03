cmake_minimum_required(VERSION 3.10)
project(cimguizmo CXX)

set(CMAKE_CXX_STANDARD 17)

# Set default build type if not defined
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

add_compile_definitions(
        NDEBUG
        CIMGUIZMO_EXPORTS
        _WINDOWS
)

# Source files
set(SOURCES
        ../../lib/cimguizmo/cimguizmo.cpp
        ../../lib/cimguizmo/ImGuizmo/GraphEditor.cpp
        ../../lib/cimguizmo/ImGuizmo/ImCurveEdit.cpp
        ../../lib/cimguizmo/ImGuizmo/ImGradient.cpp
        ../../lib/cimguizmo/ImGuizmo/ImGuizmo.cpp
        ../../lib/cimguizmo/ImGuizmo/ImSequencer.cpp

        ../../lib/cimgui/imgui/imgui.cpp
        ../../lib/cimgui/imgui/imgui_demo.cpp
        ../../lib/cimgui/imgui/imgui_draw.cpp
        ../../lib/cimgui/imgui/imgui_tables.cpp
        ../../lib/cimgui/imgui/imgui_widgets.cpp
)

# Header files
set(HEADERS
        ../../lib/cimguizmo/cimguizmo.h
)

# Include directories
include_directories(
        ../../lib/cimguizmo/ImGuizmo
        ../../lib/cimgui
        ../../lib/cimgui/imgui
)

# Create shared library
add_library(cimguizmo SHARED ${SOURCES} ${HEADERS})

# Platform-specific definitions
if(WIN32)
    target_compile_definitions(cimguizmo PRIVATE
            CIMGUIZMO_EXPORTS
            _WINDOWS
            _USRDLL
    )
else()
    target_compile_definitions(cimguizmo PRIVATE
            CIMGUIZMO_EXPORTS
    )
    set_target_properties(cimguizmo PROPERTIES PREFIX "lib")
endif()

# Output directory
set_target_properties(cimguizmo PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
        LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
        ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)