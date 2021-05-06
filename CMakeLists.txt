cmake_minimum_required(VERSION 3.19)
project(XMLValidation C)

set(CMAKE_C_STANDARD 99)

add_executable(XMLValidation main.c)

#target_include_directories(XMLValidation PRIVATE libxml)

set(CMAKE_EXE_LINKER_FLAGS -lxml2)