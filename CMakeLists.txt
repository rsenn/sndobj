project(sndobj CXX)

file(GLOB SOURCES src/*.cpp)
list(FILTER SOURCES EXCLUDE REGEX "_alt")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-write-strings")
include_directories(src include)
add_definitions(-DALSA)
add_library(sndobj ${SOURCES})
