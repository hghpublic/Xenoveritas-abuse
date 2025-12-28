cmake_minimum_required(VERSION 4.2)

project(abuse C CXX)
set(abuse_VERSION 0.9.1)
set(abuse_VERSION_MAJOR 0)
set(abuse_VERSION_MINOR 9)
set(abuse_VERSION_PATCH 1)
set(abuse_VERSION_TWEAK 0)

include(CheckIncludeFiles)

check_include_files(unistd.h HAVE_UNISTD_H)
check_include_files("sys/time.h" HAVE_SYS_TIME_H)
check_include_files("sys/ioctl.h" HAVE_SYS_IOCTL_H)
check_include_files("netinet/in.h" HAVE_NETINET_IN_H)
check_include_files(bstring.h HAVE_BSTRING_H)

set(HAVE_NETWORK TRUE CACHE BOOL "Enable networking support")

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h)

# Under Linux, match the original autotools prefix
set(ASSETDIR "data")
# Only define this for ports that actually use it
add_definitions(-DASSETDIR="${CMAKE_INSTALL_PREFIX}/${ASSETDIR}")

add_definitions(-DPACKAGE_NAME="abuse")
add_definitions(-DPACKAGE_VERSION="${abuse_VERSION}")
add_definitions(-DHAVE_CONFIG_H)
include_directories(${CMAKE_CURRENT_BINARY_DIR})

# add_definitions(-Wclass-conversion)
add_definitions(-w)

set(target abuse)
add_executable(${target})
# target_compile_options(${target} PRIVATE -Wclass-conversion)
# target_include_directories(${target} PRIVATE ${CMAKE_CURRENT_BINARY_DIR})

# copy data

add_custom_command(TARGET ${target} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory 
        ${PROJECT_SOURCE_DIR}/data
        $<TARGET_FILE_DIR:${target}>/data)

add_subdirectory(src)
# add_subdirectory(data)
