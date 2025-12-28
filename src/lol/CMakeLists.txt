set(target lol)
add_library(${target} STATIC)
target_sources(${target} PRIVATE
    matrix.cpp
    timer.cpp
)
target_include_directories(${target} PUBLIC ${PROJECT_SOURCE_DIR}/src)
