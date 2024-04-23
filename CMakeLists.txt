project(live555)
cmake_minimum_required(VERSION 3.5)

add_library(live555_interface INTERFACE)
add_library(live555::interface ALIAS live555_interface)

include(SourceList.cmake)

add_library(live555 ${LIVE555_SOURCES})

target_compile_definitions(live555 PUBLIC NO_GETIFADDRS NO_OPENSSL)

target_include_directories(live555_interface INTERFACE ${LIVE555_INTERFACE_INCLUDES})

target_link_libraries(live555 PUBLIC live555::interface)

install(TARGETS live555
            RUNTIME DESTINATION bin
            LIBRARY DESTINATION lib
            ARCHIVE DESTINATION lib)

install(FILES ${LIVE555_HEADERS} DESTINATION include/live555)
