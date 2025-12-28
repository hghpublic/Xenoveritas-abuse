
set(target sdlport)
add_library(${target} STATIC)
target_compile_definitions(${target} PRIVATE -DASSETDIR="data")
target_sources(${target} PRIVATE
    video.cpp
    event.cpp
    sound.cpp sound.h
    timing.cpp
    jdir.cpp
    joystick.cpp joy.h
    setup.cpp setup.h
    hmi.cpp hmi.h
    errorui.cpp errorui.h
)
target_include_directories(${target} PRIVATE
    ${PROJECT_SOURCE_DIR}/src
    ${PROJECT_SOURCE_DIR}/src/imlib
)

target_link_libraries(${target} PRIVATE
    $<TARGET_NAME_IF_EXISTS:SDL2::SDL2main>
    $<IF:$<TARGET_EXISTS:SDL2::SDL2>,SDL2::SDL2,SDL2::SDL2-static>
)
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:SDL2_mixer::SDL2_mixer>,
        SDL2_mixer::SDL2_mixer,
        SDL2_mixer::SDL2_mixer-static>
)
