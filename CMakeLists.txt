cmake_minimum_required(VERSION 3.2)
project(simple)

add_executable(simple simple.cpp)
target_include_directories(simple PRIVATE mpv/include)
target_link_directories(simple PRIVATE mpv)
target_link_libraries(simple libmpv-2)
set_target_properties(simple PROPERTIES 
                RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/bin/Debug
                RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/bin/Release)
add_custom_command(TARGET simple POST_BUILD                # Adds a post-build event to MyTest
                COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
                    "${PROJECT_SOURCE_DIR}/mpv/libmpv-2.dll"       # <--this is in-file
                    $<TARGET_FILE_DIR:simple>)                 # <--this is out-file path                
#install(TARGETS helloworld RUNTIME DESTINATION ${CMAKE_SOURCE_DIR})