set(HEADER_LIST "${MyProject_SOURCE_DIR}/include/say-hello/hello.h")

add_library(say-hello hello.cpp ${HEADER_LIST})

target_include_directories(say-hello PUBLIC ../include)
