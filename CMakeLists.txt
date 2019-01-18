cmake_minimum_required ( VERSION 2.8 )
set(CMAKE_VERBOSE_MAKEFILE ON)
project ( ev CXX C )

if (WIN32)
  include(configure.cmake)
  config_compiler_and_linker()
  list ( APPEND EV_LIBS Ws2_32 )
endif ()

configure_file ( ${CMAKE_CURRENT_SOURCE_DIR}/config.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/config.h )
include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${PROJECT_SOURCE_DIR})
set(LIBEV_SOURCES "ev.c;event.c")

add_library(ev_static STATIC ${LIBEV_SOURCES})
add_library(ev SHARED ${LIBEV_SOURCES})
target_include_directories (ev PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
