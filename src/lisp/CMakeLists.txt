set(target lisp)
add_library(${target} STATIC)
target_sources(${target} PRIVATE
    lisp.cpp lisp.h
    lisp_opt.cpp lisp_opt.h
    lisp_gc.cpp lisp_gc.h
    trig.cpp
    stack.h symbols.h
)
target_include_directories(${target} PRIVATE
    ${PROJECT_SOURCE_DIR}/src
    ${PROJECT_SOURCE_DIR}/src/imlib
)
target_include_directories(${target} INTERFACE ${CMAKE_CURRENT_LIST_DIR})
target_link_libraries(${target} PRIVATE
    $<TARGET_NAME_IF_EXISTS:SDL2::SDL2main>
    $<IF:$<TARGET_EXISTS:SDL2::SDL2>,SDL2::SDL2,SDL2::SDL2-static>
)
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:SDL2_mixer::SDL2_mixer>,
        SDL2_mixer::SDL2_mixer,
        SDL2_mixer::SDL2_mixer-static>
)
