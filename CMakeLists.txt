cmake_minimum_required(VERSION 3.27)
project(miniocpp)

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_VERBOSE_MAKEFILE ON)

find_package(OpenSSL REQUIRED)
find_package(nlohmann_json CONFIG REQUIRED)
find_package(pugixml CONFIG REQUIRED)
find_package(ZLIB REQUIRED)

add_subdirectory(curlpp)

set(minio_cpp_src
        src/args.cc
        src/baseclient.cc
        src/client.cc
        src/credentials.cc
        src/error.cc
        src/http.cc
        src/providers.cc
        src/request.cc
        src/response.cc
        src/select.cc
        src/signer.cc
        src/sse.cc
        src/types.cc
        src/utils.cc
        src/INIReader.cpp
        src/ini.c)

add_library(miniocpp STATIC ${minio_cpp_src})

set_target_properties(miniocpp PROPERTIES POSITION_INDEPENDENT_CODE TRUE)

target_include_directories(miniocpp
        SYSTEM PUBLIC "include/"
        SYSTEM PUBLIC "src/")

list(APPEND MINIO_CPP_LIBS
        curlpp
        nlohmann_json::nlohmann_json
        pugixml
        OpenSSL::SSL OpenSSL::Crypto
        ZLIB::ZLIB)

target_link_libraries(miniocpp PUBLIC ${MINIO_CPP_LIBS})
