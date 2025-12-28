set(target net)
add_library(${target} STATIC)
target_sources(${target} PRIVATE
    gserver.cpp gserver.h
    gclient.cpp gclient.h
    fileman.cpp fileman.h
    sock.cpp sock.h
    tcpip.cpp tcpip.h
    ghandler.h undrv.h
)

target_include_directories(${target} PRIVATE
    ${PROJECT_SOURCE_DIR}/src
    ${PROJECT_SOURCE_DIR}/src/imlib
)
target_include_directories(${target} INTERFACE ${CMAKE_CURRENT_LIST_DIR})
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:SDL2_mixer::SDL2_mixer>,
        SDL2_mixer::SDL2_mixer,
        SDL2_mixer::SDL2_mixer-static>
)

target_compile_definitions(${target} PRIVATE -DNO_CHECK)
