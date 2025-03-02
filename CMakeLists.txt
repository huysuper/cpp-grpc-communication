cmake_minimum_required(VERSION 3.10.0)
project(Cpp-gRPC-Practice VERSION 0.1.0 LANGUAGES C CXX)

add_subdirectory(client)
add_subdirectory(server)

include(CTest)
enable_testing()

