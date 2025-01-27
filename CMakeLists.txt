cmake_minimum_required(VERSION 3.27)
project(
  mesh_simplification
  VERSION 1.0.0
  LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

if(MSVC)
  add_compile_options(/W4 /WX)
  if(CMAKE_BUILD_TYPE STREQUAL Debug)
    add_compile_options(/fsanitize=address)
  else()
    add_compile_options(/Ob3 /GL)
    add_link_options(/LTCG:INCREMENTAL)
  endif()
else()
  add_compile_options(-Wall -Werror -Wextra -Wpedantic)
  if(CMAKE_BUILD_TYPE STREQUAL Debug)
    add_compile_options(-fsanitize=address)
    add_link_options(-fsanitize=address)
  else()
    add_compile_options(-O3 -flto)
    add_link_options(-flto)
  endif()
endif()

add_subdirectory(src)

enable_testing()
add_subdirectory(tests)
