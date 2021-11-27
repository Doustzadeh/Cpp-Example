cmake_minimum_required(VERSION 3.20)

# set the project name
project(Hello-wxWidgets)

set(SOURCE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp)

set(WX "C:/wxWidgets-3.1.5")
set(MINGW_HOME "C:/mingw32")

include_directories("${WX}/include")

link_directories("${WX}/lib/gcc_lib")
link_directories("${MINGW_HOME}/i686-w64-mingw32/lib")

set(LIB_FILES kernel32 user32 gdi32 winspool comdlg32 advapi32 shell32 ole32 oleaut32 uuid comctl32 wsock32 odbc32 shlwapi version oleacc uxtheme)

if (CMAKE_BUILD_TYPE STREQUAL "Debug")
    # Do something only for debug builds
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/debug)

    if(WIN32)
        include_directories("${WX}/lib/gcc_lib/mswud")
        link_directories("${WX}/lib/gcc_lib/mswud")
    endif()

    set(LIB_FILES ${LIB_FILES} wxmsw31ud_core wxbase31ud wxbase31ud_net wxpngd wxjpegd wxtiffd wxzlibd)
elseif (CMAKE_BUILD_TYPE STREQUAL "Release")
    # Do something only for release builds
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/release)

    if(WIN32)
        include_directories("${WX}/lib/gcc_lib/mswu")
        link_directories("${WX}/lib/gcc_lib/mswu")
    endif()

    set(LIB_FILES ${LIB_FILES} wxmsw31u_core wxbase31u wxbase31u_net wxpng wxjpeg wxtiff wxzlib)
endif ()

link_libraries(${LIB_FILES})


set(CMAKE_SYSTEM_PROCESSOR i686)
set(CMAKE_CXX_COMPILER g++)

set(CMAKE_CXX_FLAGS_INIT -m32)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -pipe -mthreads -D__GNUWIN32__ -D__WXMSW__ -DwxUSE_UNICODE")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g -O0")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O2 -DNDEBUG -s")

set(CMAKE_LINKER_FLAGS "${CMAKE_LINKER_FLAGS} -static-libstdc++ -static-libgcc -mthreads")
set(CMAKE_DEBUG_LINKER_FLAGS "${CMAKE_DEBUG_LINKER_FLAGS} -g")

set(CMAKE_EXE_LINKER_FLAGS_INIT -m32)

if(WIN32 AND CMAKE_BUILD_TYPE STREQUAL "Release")
    # if set WIN32 -> disabled console log -> std::out not working
    add_executable(${CMAKE_PROJECT_NAME} WIN32 ${SOURCE_FILES})
else()
    add_executable(${CMAKE_PROJECT_NAME} ${SOURCE_FILES})
endif()

target_link_libraries(${CMAKE_PROJECT_NAME} ${LIB_FILES})
