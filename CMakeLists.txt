cmake_minimum_required(VERSION 3.18)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)
project(OpenSA)

option(OPENSA_DEBUG "Enable developer mode" False)

if (${OPENSA_DEBUG} EQUAL True)
    set(HOOK_RT_DEBUG True)
endif()

configure_file(SA_Config.h.in SA_Config.h)

add_subdirectory(lib/BL-RuntimeA64v8a)
include_directories(${CMAKE_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR})

add_library(OpenSA SHARED)
target_sources(OpenSA PRIVATE plugin_load_thread.cpp 
    opensa_logger.cpp 
    Virtual_ENV.cpp
    game/Game_Context.cpp 
    game/Hooks_Cortex.cpp
    game/MainMenu_Hooks.cpp)

target_link_libraries(OpenSA blrta64 log)
