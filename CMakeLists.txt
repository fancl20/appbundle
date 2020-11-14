cmake_minimum_required(VERSION 3.18)
project(akashic)

set(CMAKE_CXX_STANDARD 20)
add_subdirectory(third_party)

using(meson VERSION 0.56.0)
using(ninja VERSION 1.10.1)
using(libfuse VERSION 3.10.0)
find_package(Threads REQUIRED)

add_executable(appbundle main.cc)
target_compile_options(appbundle PRIVATE
    -O2 -g -Wall -Wextra -Werror -Wpedantic
)
set(STATIC_LINK_LIBCXX -static)
if (APPLE)
    unset(STATIC_LINK_LIBCXX)
endif()
target_link_libraries(appbundle
    libfuse
    Threads::Threads ${STATIC_LINK_LIBCXX}
)