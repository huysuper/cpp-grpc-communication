cmake_minimum_required(VERSION 3.10.0)
project(Cpp-gRPC-Practice VERSION 0.1.0 LANGUAGES C CXX)

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/CMakeModules")
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

include(FetchContent)
include(Abseil)
include(gRPC)

add_subdirectory(protos)
add_subdirectory(client)
add_subdirectory(server)

include(CTest)
enable_testing()

