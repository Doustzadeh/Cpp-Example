cmake_minimum_required(VERSION 3.20)

# set the project name and version
project(Hello-Sciter)

set(SOURCE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp)

set(SCITER_SDK "C:/sciter-js-sdk")
set(MINGW_HOME "C:/Program Files (x86)/CodeBlocks/MinGW")

include_directories("${SCITER_SDK}/include")
include_directories("${MINGW_HOME}/opt/include")


link_directories("${MINGW_HOME}/i686-w64-mingw32/lib")
set(LIB_FILES ole32)
link_libraries(${LIB_FILES})


set(CMAKE_CXX_STANDARD 14)

set(CMAKE_SYSTEM_PROCESSOR i686)
set(CMAKE_CXX_COMPILER g++)

set(CMAKE_CXX_FLAGS_INIT -m32)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fmessage-length=0 -Wall -fexceptions")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g -O0")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O2 -DNDEBUG -s")

set(CMAKE_LINKER_FLAGS "${CMAKE_LINKER_FLAGS} -municode")
set(CMAKE_DEBUG_LINKER_FLAGS "${CMAKE_DEBUG_LINKER_FLAGS} -g")

set(CMAKE_EXE_LINKER_FLAGS_INIT -m32)


if(WIN32)
    execute_process(COMMAND cmd /c 
                    ${SCITER_SDK}/bin/windows/packfolder.exe 
                    ${CMAKE_CURRENT_SOURCE_DIR}/res 
                    ${CMAKE_CURRENT_SOURCE_DIR}/src/resources.cpp 
                    -v "resources")
endif()


if (CMAKE_BUILD_TYPE STREQUAL "Debug")
    # Do something only for debug builds
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/debug)
    file(COPY ${SCITER_SDK}/bin/windows/x32/sciter.dll DESTINATION ${CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG}/)
elseif (CMAKE_BUILD_TYPE STREQUAL "Release")
    # Do something only for release builds
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/release)
    file(COPY ${SCITER_SDK}/bin/windows/x32/sciter.dll DESTINATION ${CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE}/)
endif ()


add_executable(${CMAKE_PROJECT_NAME} ${SOURCE_FILES})
