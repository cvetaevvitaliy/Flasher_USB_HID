cmake_minimum_required(VERSION 3.16)
project(CLI_HID C)

set(CMAKE_C_STANDARD 99)

if(WIN32)
    message( "Detect WIN32" )
    message( "Please add library patch for Windows build" )

elseif(APPLE)
    message( "Detect Mac OS" )

    file(GLOB_RECURSE SOURCES hid-mac.c )
    find_library( COREFOUNDATION_LIBRARY CoreFoundation )
    find_library( IOKIT_LIBRARY IOKit )
    set (LIBARIES ${IOKIT_LIBRARY} ${COREFOUNDATION_LIBRARY})
elseif(LINUX)
    message( "Detect Linux" )
    message( "Please add library patch for Linux build" )
endif()

SET(CMAKE_CXX_FLAGS_INIT " -std=c++11")
SET(CMAKE_C_FLAGS_INIT "-std=gnu99")


add_executable(${PROJECT_NAME} main.c ${SOURCES})
target_link_libraries(${PROJECT_NAME} ${LIBARIES})