cmake_minimum_required ( VERSION 2.8 )
set(CMAKE_VERBOSE_MAKEFILE ON)
project ( ev CXX C )

include(configure.cmake)
config_compiler_and_linker()

configure_file ( ${CMAKE_CURRENT_SOURCE_DIR}/config.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/config.h )
include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${PROJECT_SOURCE_DIR})
set(LIBEV_SOURCES "ev.c;event.c")

if (WIN32) 
  list ( APPEND EV_LIBS Ws2_32 )
endif ()

# build libkcpev
add_library(ev_static STATIC ${LIBEV_SOURCES})
target_link_libraries(libev_static ${EV_LIBS})

add_library(ev SHARED ${LIBEV_SOURCES})
target_link_libraries(libev ${EV_LIBS})

