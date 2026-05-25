cmake_minimum_required(VERSION 3.13)

include(pico_sdk_import.cmake)

project(pico2w_bt_remote C CXX ASM)

pico_sdk_init()

add_executable(pico2w_bt_remote Bluetooth_trebuche.cpp)

# Generate GATT header from .gatt file
pico_btstack_make_gatt_header(pico2w_bt_remote remote_service.gatt)

# Link libraries for Pico 2 W Bluetooth
target_link_libraries(pico2w_bt_remote 
    pico_stdlib 
    pico_cyw43_arch_none 
    pico_btstack_ble 
    pico_btstack_cyw43 
    hardware_uart
)

# Enable USB output for printf debugging
pico_enable_stdio_usb(pico2w_bt_remote 1)
pico_enable_stdio_uart(pico2w_bt_remote 0)

pico_add_extra_outputs(pico2w_bt_remote)
# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.2.0)
set(toolchainVersion 14_2_Rel1)
set(picotoolVersion 2.2.0-a4)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================