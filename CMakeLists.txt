cmake_minimum_required(VERSION 3.12)

include(pico_sdk_import.cmake)

set(project_name "fatfs_test")
project(${project_name})
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

pico_sdk_init()

add_subdirectory(fatfs)
add_subdirectory(hardware_gpio_ex)

set(bin_name "fatfs_test")
add_executable(${bin_name}
    main.cpp
)

pico_enable_stdio_usb(${bin_name} 0)
pico_enable_stdio_uart(${bin_name} 1)

target_link_libraries(${bin_name} PRIVATE
    pico_stdlib
    hardware_uart
    hardware_gpio_ex
    fatfs
)
pico_add_extra_outputs(${bin_name})
