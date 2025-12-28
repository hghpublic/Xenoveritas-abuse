find_package(SDL2 CONFIG REQUIRED)
find_package(SDL2_mixer CONFIG REQUIRED)

add_subdirectory(lol)

# SUBDIRS = lisp net imlib sdlport
add_subdirectory(lisp)
add_subdirectory(imlib)
add_subdirectory(net)
add_subdirectory(sdlport)


set(target abuse)
# add_executable(${target})
target_sources(${target} PRIVATE
    common.h
    lol/matrix.cpp lol/matrix.h
    lol/timer.cpp lol/timer.h
    specache.cpp specache.h
    netcfg.cpp netcfg.h
    innet.cpp
    chat.cpp chat.h
    endgame.cpp
    loadgame.cpp loadgame.h
    profile.cpp profile.h
    cop.cpp cop.h
    statbar.cpp
    compiled.cpp compiled.h
    ant.cpp ant.h
    sensor.cpp
    demo.cpp demo.h
    lcache.cpp lcache.h
    nfclient.cpp nfclient.h
    clisp.cpp clisp.h
    gui.cpp gui.h
    transp.cpp transp.h
    collide.cpp
    property.cpp property.h
    cache.cpp cache.h
    particle.cpp particle.h
    objects.cpp objects.h
    extend.cpp extend.h
    console.cpp console.h
    ability.cpp ability.h
    items.cpp items.h
    dev.cpp dev.h
    chars.cpp chars.h
    level.cpp level.h
    smallfnt.cpp
    automap.cpp automap.h
    help.cpp help.h
    intsect.cpp intsect.h
    loader2.cpp loader2.h
    seq.cpp seq.h
    points.cpp points.h
    fnt6x13.cpp
    morpher.cpp morpher.h
    menu.cpp menu.h
    director.cpp director.h
    view.cpp view.h
    configuration.cpp configuration.h
    game.cpp game.h
    light.cpp light.h
    devsel.cpp devsel.h
    crc.cpp crc.h
    gamma.cpp gamma.h
    id.h netface.h isllist.h sbar.h
    nfserver.h
    ui/volumewindow.cpp ui/volumewindow.h
)

target_link_libraries(${target} PRIVATE lisp)
target_link_libraries(${target} PRIVATE sdlport)
target_link_libraries(${target} PRIVATE imlib)
target_link_libraries(${target} PRIVATE net)

target_link_libraries(${target} PRIVATE
    $<TARGET_NAME_IF_EXISTS:SDL2::SDL2main>
    $<IF:$<TARGET_EXISTS:SDL2::SDL2>,SDL2::SDL2,SDL2::SDL2-static>
)
target_link_libraries(${target} PRIVATE
    $<IF:$<TARGET_EXISTS:SDL2_mixer::SDL2_mixer>,
        SDL2_mixer::SDL2_mixer,
        SDL2_mixer::SDL2_mixer-static>
)

if(OPENGL_FOUND)
    target_link_libraries(${target} ${OPENGL_LIBRARIES})
endif(OPENGL_FOUND)

target_include_directories(${target} PRIVATE ${CMAKE_CURRENT_LIST_DIR})

if(false)
set(target abuse-tool)
add_executable(${target})
target_sources(${target} PRIVATE
    tool/abuse-tool.cpp
    crc.cpp
    crc.h
)

target_link_libraries(${target} PRIVATE imlib)

include_directories(
    ${abuse_SOURCE_DIR}/src
    ${abuse_SOURCE_DIR}/src/lisp
    ${abuse_SOURCE_DIR}/src/imlib
    ${abuse_SOURCE_DIR}/src/net
    ${SDL2_INCLUDE_DIR}
    ${SDL2_MIXER_INCLUDE_DIR}
)
endif()
