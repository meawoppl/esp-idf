cmake_minimum_required(VERSION 3.16)

set(PROTO_COMPILER "protoc")
set(PROTO_C_COMPILER "protoc-c")
set(C_OUT_PATH "${CMAKE_CURRENT_LIST_DIR}/../proto-c")
set(PY_OUT_PATH "${CMAKE_CURRENT_LIST_DIR}/../python")

set(PROTO_SRCS "constants.proto"
               "sec0.proto"
               "sec1.proto"
               "session.proto")

add_custom_target(c_proto
    COMMAND ${PROTO_C_COMPILER} --c_out=${C_OUT_PATH} -I . ${PROTO_SRCS}
    VERBATIM
    WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
    )

add_custom_target(python_proto
    COMMAND ${PROTO_COMPILER} --python_out=${PY_OUT_PATH} -I . ${PROTO_SRCS}
    VERBATIM
    WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
    )

add_custom_target(proto ALL
    DEPENDS c_proto python_proto
    VERBATIM
    WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
    )
