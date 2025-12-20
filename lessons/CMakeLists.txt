cmake_minimum_required(VERSION 4.2)

project(lessons LANGUAGES C)

find_package(raylib CONFIG REQUIRED)
find_package(glfw3 CONFIG REQUIRED)

set(targets
    01_blocks_game_intro
    02_blocks_game_drawing
    03_blocks_game_inputs
    04_blocks_game_collisions
    05_blocks_game_textures
    06_blocks_game_text
    07_blocks_game_audio
)

foreach(target IN LISTS targets)
add_executable(${target})
target_sources(${target} PRIVATE ${target}.c)
target_link_libraries(${target} PRIVATE raylib)
target_link_libraries(${target} PRIVATE glfw)
target_link_libraries(${target} PRIVATE m)    
endforeach()

# copy resources

set(target 01_blocks_game_intro)
add_custom_command(TARGET ${target} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory 
        ${CMAKE_CURRENT_SOURCE_DIR}/resources
        $<TARGET_FILE_DIR:${target}>/resources
)