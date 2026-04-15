cmake_minimum_required(VERSION 3.10)

project(Caravan)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

find_package(SDL3 CONFIG REQUIRED)
find_package(glad CONFIG REQUIRED)

add_executable(Caravan src/main.cpp)

target_link_libraries(Caravan PRIVATE SDL3::SDL3)
target_link_libraries(Caravan PRIVATE glad::glad)
