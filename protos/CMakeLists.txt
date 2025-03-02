macro(add_proto library_name proto_src)
  # Proto file
  get_filename_component(${library_name}_proto "${proto_src}.proto" ABSOLUTE)
  get_filename_component(${library_name}_proto_path "${${library_name}_proto}" PATH)

  # Generated sources
  set(${library_name}_proto_srcs "${CMAKE_CURRENT_BINARY_DIR}/${proto_src}.pb.cc")
  set(${library_name}_proto_hdrs "${CMAKE_CURRENT_BINARY_DIR}/${proto_src}.pb.h")
  set(${library_name}_grpc_srcs "${CMAKE_CURRENT_BINARY_DIR}/${proto_src}.grpc.pb.cc")
  set(${library_name}_grpc_hdrs "${CMAKE_CURRENT_BINARY_DIR}/${proto_src}.grpc.pb.h")
  add_custom_command(
        OUTPUT "${${library_name}_proto_srcs}" "${${library_name}_proto_hdrs}" "${${library_name}_grpc_srcs}" "${${library_name}_grpc_hdrs}"
        COMMAND ${_PROTOBUF_PROTOC}
        ARGS  --grpc_out "${CMAKE_CURRENT_BINARY_DIR}"
              --cpp_out "${CMAKE_CURRENT_BINARY_DIR}"
              -I "${${library_name}_proto_path}"
              --plugin=protoc-gen-grpc="${_GRPC_CPP_PLUGIN_EXECUTABLE}"
              "${${library_name}_proto}"
        DEPENDS "${${library_name}_proto}")

  # Add libraries
  add_library(${library_name}
    ${${library_name}_grpc_srcs}
    ${${library_name}_grpc_hdrs}
    ${${library_name}_proto_srcs}
    ${${library_name}_proto_hdrs})
  target_include_directories(${library_name} PUBLIC "${CMAKE_CURRENT_BINARY_DIR}")
  target_link_libraries(${library_name}
    absl::check
    protobuf::libprotobuf
    grpc++_reflection
    grpc++
  )
endmacro()

add_proto(protos_helloworld
  "helloworld"
)

