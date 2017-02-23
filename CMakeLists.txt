cmake_minimum_required (VERSION 2.8)
project (webrtc_client)


set (PLATFORM "client")

message("Build for :" ${PLATFORM}":")


set (CMAKE_SKIP_RPATH 1)

if(WIN32)
    file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/win32/*
     DESTINATION ${CMAKE_CURRENT_SOURCE_DIR}/src)
else()
    file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/src/linux/*
     DESTINATION ${CMAKE_CURRENT_SOURCE_DIR}/src)
endif()


#include_directories("${PROJECT_SOURCE_DIR}/videoencoder_${PLATFORM}")

#include_directories ("${PROJECT_BINARY_DIR}")

file(GLOB client_SRC 
    "src/*.h"
    "src/*.cc"
)

add_executable (webrtc_client ${client_SRC})

target_include_directories(webrtc_client PUBLIC "/usr/local/cuda/include")
target_link_libraries(webrtc_client jingle_peerconnection )


