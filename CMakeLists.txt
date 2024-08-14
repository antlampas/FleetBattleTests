cmake_minimum_required(VERSION 3.15)

project(FleetBattleTests
        VERSION "${VERSION}"
        DESCRIPTION "Tests for FALP Fleet Battle"
        HOMEPAGE_URL "https://github.com/antlampas/FleetBattleTests"
        LANGUAGES "CXX")

include(CTest)
include(FetchContent)

FetchContent_Declare(
  fleetbattle
  GIT_REPOSITORY https://github.com/antlampas/FleetBattle.git
  GIT_BRANCH     master
)

FetchContent_Declare(
  Catch2
  GIT_REPOSITORY https://github.com/catchorg/Catch2.git
  GIT_TAG        v3.6.0
)

FetchContent_MakeAvailable(fleetbattle catch2)

if("${CMAKE_BUILD_TYPE}" MATCHES "Debug")
add_definitions(-DDEBUG)
endif()

include_directories(${CMAKE_CURRENT_BINARY_DIR}/_deps/fleetbattle-src/include)

add_subdirectory(src          ${CMAKE_BUILD_TYPE}/Tests)
