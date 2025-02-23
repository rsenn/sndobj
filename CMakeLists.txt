project(sndobj C CXX)

option(USE_JACK "Use jack" ON)

if(USE_JACK)
  add_definitions(-DJACK)
  link_libraries(jack)
endif(USE_JACK)

link_libraries(asound)

file(GLOB RFFTW_SOURCES src/rfftw/*.c)
message(STATUS "RFFTW_SOURCES: ${RFFTW_SOURCES}")
file(GLOB SOURCES src/*.cpp)

list(FILTER SOURCES EXCLUDE REGEX "FFT_alt")

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-write-strings")

if(${CMAKE_BUILD_TYPE} STREQUAL "Debug")
  add_definitions(-DDEBUG)
endif(${CMAKE_BUILD_TYPE} STREQUAL "Debug")

include_directories(src include include/rfftw)
add_definitions(-DALSA)
# add_library(rfftw STATIC ${RFFTW_SOURCES})
add_library(sndobj SHARED ${SOURCES} ${RFFTW_SOURCES})
# target_link_libraries(sndobj rfftw)
