cmake_minimum_required(VERSION 3.8 FATAL_ERROR) 
project(realm_of_shadows CXX)

add_subdirectory(lib/imgui EXCLUDE_FROM_ALL)
add_subdirectory(lib/gl3w EXCLUDE_FROM_ALL)
add_subdirectory(lib/glfw EXCLUDE_FROM_ALL)

# Host
add_executable(host "")

target_sources(host
    PRIVATE
    src/host.cpp
    src/fswatcher/fswatcher.cpp
    src/fswatcher/fswatcher.h
)

target_include_directories(host
    PRIVATE
    lib/imgui
    lib/gl3w
    lib/glfw
)

target_link_libraries(host 
    PRIVATE 
    imgui
    gl3w
    glfw
)

# Guest
add_library(guest SHARED "")

target_sources(guest
    PRIVATE
    src/guest.cpp
)

target_include_directories(guest
    PRIVATE
    lib/imgui
    lib/gl3w
    lib/glfw
    src/fswatcher
)

target_link_libraries(guest 
    PRIVATE 
    imgui
    gl3w
    glfw
)

# Windows
if (${CMAKE_CXX_COMPILER_ID} STREQUAL MSVC)
    target_link_libraries(host PRIVATE opengl32.lib)
    target_link_libraries(guest PRIVATE opengl32.lib)


    target_compile_options(host PRIVATE 
    PUBLIC
        -permissive- -std:c++17
    PRIVATE
        -WX- -W4
    )

    target_compile_options(guest PRIVATE 
    PUBLIC
        -permissive- -std:c++17
    PRIVATE
        -WX- -W4
    )
endif()

SET(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/${CMAKE_BUILD_TYPE} CACHE PATH "Library output path")
SET(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/${CMAKE_BUILD_TYPE} CACHE PATH "Executable output path")
add_definitions (-DGUEST_DLL_PATH="${CMAKE_BINARY_DIR}/Debug/guest.dll")
