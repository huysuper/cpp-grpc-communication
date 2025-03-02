cmake_minimum_required(VERSION 3.10.0)
project(server VERSION 0.1.0 LANGUAGES C CXX)

add_executable(server main.cpp)

target_link_libraries(server 
    grpc++
    absl::strings
    absl::flags
    absl::flags_parse
    protos_helloworld
)