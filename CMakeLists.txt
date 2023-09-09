cmake_minimum_required(VERSION 3.15)

project(asio)

include(FetchContent)

FetchContent_Declare(asioftch
  GIT_REPOSITORY  https://github.com/chriskohlhoff/asio.git
  GIT_TAG         master
  GIT_SHALLOW     TRUE
)

FetchContent_GetProperties(asioftch)

if(NOT asioftch_POPULATED)
  FetchContent_Populate(asioftch)
  
  message(STATUS "Populated asio")
endif()

add_library(asio INTERFACE)

target_include_directories(asio
  INTERFACE "${asioftch_SOURCE_DIR}/asio/include"
)

target_sources(asio
  "${asioftch_SOURCE_DIR}/asio/src/asio.cpp"
  "${asioftch_SOURCE_DIR}/asio/src/asio_ssl.cpp"
)

target_compile_definitions(asio
  INTERFACE
    ASIO_STANDALONE
    ASIO_NO_DEPRECATED
)

if(WIN32)
  set(_WIN32_WINNT "0x0601")
  message(STATUS "Setting up for Windows 7")

  target_compile_definitions(asio
    INTERFACE
      _WIN32_WINNT=${_WIN32_WINNT}
      WIN32_LEAN_AND_MEAN
  )
endif()

find_package(Threads REQUIRED)

target_link_libraries(asio Threads::Threads)
