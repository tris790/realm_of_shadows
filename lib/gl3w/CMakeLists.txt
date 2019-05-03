cmake_minimum_required (VERSION 3.8)
project (gl3w)

include_directories(.)

set(GL3W_SOURCES
    "gl3w.c"
)

set(GL3W_HEADERS
    "GL/gl3w.h"
    "GL/glcorearb.h"
    "KHR/khrplatform.h"
)

add_library(gl3w ${GL3W_SOURCES} ${GL3W_HEADERS})