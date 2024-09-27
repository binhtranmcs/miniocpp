
message(STATUS "Looking for CURL")
find_package(CURL REQUIRED)

if(CURL_FOUND)
  message(STATUS "Found CURL version: ${CURL_VERSION_STRING}")
  message(STATUS "Using CURL include dir(s): ${CURL_INCLUDE_DIRS}")
  message(STATUS "Using CURL lib(s): ${CURL_LIBRARIES}")
else()
  message(STATUS "Fetching CURL")
  include(FetchContent)
  FetchContent_Declare(CURL GIT_REPOSITORY https://github.com/curl/curl.git)
  FetchContent_MakeAvailable(CURL)
endif()

# All following targets should search these directories for headers
include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}/include
  ${CURL_INCLUDE_DIRS}
)

file(GLOB_RECURSE HeaderFileList "${CMAKE_CURRENT_SOURCE_DIR}/include/*")
file(GLOB_RECURSE SourceFileList "${CMAKE_CURRENT_SOURCE_DIR}/src/*")

add_library(curlpp STATIC ${HeaderFileList} ${SourceFileList})
target_include_directories(curlpp PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")

target_link_libraries(curlpp ${CURL_LIBRARIES})

set_target_properties(curlpp PROPERTIES POSITION_INDEPENDENT_CODE TRUE)
