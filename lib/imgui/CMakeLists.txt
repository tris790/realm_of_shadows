cmake_minimum_required (VERSION 3.5.1)
project (imgui)

set(IMGUI_SOURCES
    "imgui.cpp"
    "imgui_demo.cpp"
    "imgui_draw.cpp"
    "imgui_widgets.cpp"
)

set(IMGUI_HEADERS
    "imconfig.h"
    "imgui_internal.h"
    "imgui.h"
    "imstb_rectpack.h"
    "imstb_textedit.h"
    "imstb_truetype.h"
)

add_library(imgui ${IMGUI_SOURCES} ${IMGUI_HEADERS})