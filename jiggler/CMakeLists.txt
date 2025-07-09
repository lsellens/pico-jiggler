# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.1.1)
set(toolchainVersion 14_2_Rel1)
set(picotoolVersion 2.1.1)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
set(PICO_BOARD pico2 CACHE STRING "Board type")

add_executable(jiggler
        jiggler.c
        usb_descriptors.c
        )

target_include_directories(jiggler PRIVATE ${CMAKE_CURRENT_LIST_DIR})

target_link_libraries(jiggler PRIVATE pico_stdlib tinyusb_device tinyusb_board)
pico_add_extra_outputs(jiggler)

pico_set_program_url(jiggler https://github.com/argilo/pico-jiggler)
