cmake_minimum_required(VERSION 3.25.1)
project(omni_types)

list(PREPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/../../cmake)

include(CPM)
include(CTest)

enable_testing()

find_package(PostgreSQL REQUIRED)

add_postgresql_extension(
        omni_types
        VERSION 0.1
        SCHEMA omni_types
        RELOCATABLE false
        SCRIPTS omni_types--0.1.sql
        SOURCES omni_types.c unit.c sum_type.c
        REGRESS unit sum_type
)

add_library(libomnitypes INTERFACE)
target_include_directories(libomnitypes INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})
