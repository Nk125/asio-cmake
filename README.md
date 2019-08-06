# ASIO CMake

ASIO-CMake provides handy cmake pacakage wrapper for using asio.

## Quick Start

We use CMake module [FetchContent](https://cmake.org/cmake/help/latest/module/FetchContent.html) to enable dependency populating, thus CMake v3.11 at minimum is required.

```cmake
include(FetchContent)

FetchContent_Declare(asio-cmake
  GIT_REPOSITORY https://github.com/kingsamchen/asio-cmake.git
  GIT_TAG        origin/master
)

# Specify asio version
set(ASIO_CMAKE_ASIO_TAG asio-1-12-2)
FetchContent_MakeAvailable(asio-cmake)

# ...

target_link_libraries(proj-name
  PRIVATE asio
)
```

NOTE: `FetchContent_MakeAvailable()` is usable since CMake 3.14; but you can use other population commands for lower versions.

## Motivation

For integrating ASIO in CMake projects easier.

Make ASIO && C++ Great Again.