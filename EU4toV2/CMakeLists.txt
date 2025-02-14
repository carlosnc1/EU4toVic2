cmake_minimum_required(VERSION 3.5)
#set(CMAKE_VERBOSE_MAKEFILE on)

project(EU4ToVic2)
SET(CMAKE_CXX_COMPILER g++-7)
set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/Source)
set(PROJECT_SOURCE_DIR ${CMAKE_SOURCE_DIR}/Source)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/Release-Linux)
set(LIBRARY_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/Release-Linux)

add_compile_options("-std=c++17")
add_compile_options("-g")

include_directories("../common_items")
include_directories("${PROJECT_SOURCE_DIR}")

file(GLOB MAIN_SOURCES "${PROJECT_SOURCE_DIR}/*.cpp")
file(GLOB VIC2WORLD_SOURCES "${PROJECT_SOURCE_DIR}/V2World/*.cpp")
file(GLOB HELPER_SOURCES "${PROJECT_SOURCE_DIR}/Helpers/*.cpp")
file(GLOB MAPPER_SOURCES "${PROJECT_SOURCE_DIR}/Mappers/*.cpp")
file(GLOB IDEAS_MAPPER_SOURCES "${PROJECT_SOURCE_DIR}/Mappers/Ideas/*.cpp")
file(GLOB PROVINCE_MAPPER_SOURCES "${PROJECT_SOURCE_DIR}/Mappers/ProvinceMappings/*.cpp")
file(GLOB EU4_WORLD_SOURCES "${PROJECT_SOURCE_DIR}/EU4World/*.cpp")
file(GLOB EU4_BUILDINGS_SOURCES "${PROJECT_SOURCE_DIR}/EU4World/Buildings/*.cpp")
file(GLOB EU4_MODS_SOURCES "${PROJECT_SOURCE_DIR}/EU4World/Mods/*.cpp")
file(GLOB EU4_MODIFIERS_SOURCES "${PROJECT_SOURCE_DIR}/EU4World/Modifiers/*.cpp")
file(GLOB EU4_PROVINCES_SOURCES "${PROJECT_SOURCE_DIR}/EU4World/Provinces/*.cpp")
file(GLOB EU4_REGIONS_SOURCES "${PROJECT_SOURCE_DIR}/EU4World/Regions/*.cpp")
file(GLOB EU4_RELIGIONS_SOURCES "${PROJECT_SOURCE_DIR}/EU4World/Religions/*.cpp")
set(COMMON_SOURCES "../common_items/CardinalToOrdinal.cpp")
set(COMMON_SOURCES ${COMMON_SOURCES} "../common_items/Color.cpp")
set(COMMON_SOURCES ${COMMON_SOURCES} "../common_items/CommonUtils.cpp")
set(COMMON_SOURCES ${COMMON_SOURCES} "../common_items/Date.cpp")
set(COMMON_SOURCES ${COMMON_SOURCES} "../common_items/LinuxUtils.cpp")
set(COMMON_SOURCES ${COMMON_SOURCES} "../common_items/Log.cpp")
set(COMMON_SOURCES ${COMMON_SOURCES} "../common_items/Object.cpp")
set(COMMON_SOURCES ${COMMON_SOURCES} "../common_items/newParser.cpp")
set(COMMON_SOURCES ${COMMON_SOURCES} "../common_items/NewParserToOldParserConverters.cpp")
set(COMMON_SOURCES ${COMMON_SOURCES} "../common_items/ParadoxParser8859_15.cpp")
set(COMMON_SOURCES ${COMMON_SOURCES} "../common_items/ParadoxParserUTF8.cpp")
set(COMMON_SOURCES ${COMMON_SOURCES} "../common_items/ParserHelpers.cpp")

set(Boost_USE_STATIC_LIBS       OFF)
set(Boost_USE_MULTITHREADED     OFF)
set(Boost_USE_STATIC_RUNTIME    OFF)
find_package(Boost)
if(Boost_FOUND)
  add_executable(EU4ToVic2 ${MAIN_SOURCES} ${VIC2WORLD_SOURCES} ${HELPER_SOURCES} ${MAPPER_SOURCES} ${IDEAS_MAPPER_SOURCES} ${PROVINCE_MAPPER_SOURCES} ${EU4_WORLD_SOURCES} ${EU4_BUILDINGS_SOURCES} ${EU4_MODS_SOURCES} ${EU4_MODIFIERS_SOURCES} ${EU4_PROVINCES_SOURCES} ${EU4_REGIONS_SOURCES} ${EU4_RELIGIONS_SOURCES} ${COMMON_SOURCES})
  add_custom_command(TARGET EU4ToVic2 POST_BUILD WORKING_DIRECTORY ${CMAKE_SOURCE_DIR} COMMAND chmod u+x Copy_Files.sh)
  add_custom_command(TARGET EU4ToVic2 POST_BUILD WORKING_DIRECTORY ${CMAKE_SOURCE_DIR} COMMAND ./Copy_Files.sh)
endif()