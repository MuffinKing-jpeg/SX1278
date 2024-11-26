cmake_minimum_required(VERSION 3.22)

project(sx1278)
add_library(sx1278 INTERFACE)

# Enable CMake support for ASM and C languages
enable_language(C ASM)


message("SX1278 driver
Author: Wojciech Domski
Git: https://github.com/wdomski

Cmake integration: Andrii Dobrus
Git: https://github.com/MuffinKing-jpeg
")

file(GLOB SX1278_SRC_FILES ${CMAKE_CURRENT_SOURCE_DIR}/driver/*.c)

target_include_directories(sx1278 INTERFACE
${CMAKE_CURRENT_SOURCE_DIR}/driver
)

target_sources(sx1278 PUBLIC
    ${SX1278_SRC_FILES}
    # Add user sources here
)

target_link_directories(sx1278 INTERFACE
)

target_link_libraries(sx1278 INTERFACE
)

# Validate that STM32CubeMX code is compatible with C standard
if(CMAKE_C_STANDARD LESS 11)
    message(ERROR "Generated code requires C11 or higher")
endif()