cmake_minimum_required(VERSION 3.13)

# initialize the SDK based on PICO_SDK_PATH
# note: this must happen before project()
include(pico_sdk_import.cmake)

project(coremark)

# initialize the Raspberry Pi Pico SDK
pico_sdk_init()

add_executable(coremark
    core_list_join.c
    core_main.c
    core_matrix.c
    core_state.c
    core_util.c
    simple/core_portme.c
)

target_compile_definitions(coremark PRIVATE
    ITERATIONS=0
    FLAGS_STR="-O3"
)

target_include_directories(coremark PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}
    ${CMAKE_CURRENT_LIST_DIR}/simple/
)

# Add pico_stdlib library which aggregates commonly used features
target_link_libraries(coremark pico_stdlib)

# create map/bin/hex/uf2 file in addition to ELF.
pico_add_extra_outputs(coremark)
