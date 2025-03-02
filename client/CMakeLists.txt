cmake_minimum_required(VERSION 3.10.0)
project(client VERSION 0.1.0 LANGUAGES C CXX)

add_executable(client main.cpp)

target_link_libraries(client 
    grpc++
    absl::strings
    absl::flags
    absl::flags_parse
    protos_helloworld
)