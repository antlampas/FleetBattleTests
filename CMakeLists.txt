cmake_minimum_required(VERSION 3.15)

project(FleetBattleTests
        VERSION "${VERSION}"
        DESCRIPTION "Tests for Fleet Battle 2"
        HOMEPAGE_URL "https://github.com/antlampas/FleetBattleTests"
        LANGUAGES "CXX")

include(CTest)
include(FetchContent)

FetchContent_Declare(
  fleetbattle
  GIT_REPOSITORY https://github.com/antlampas/FleetBattle.git
  GIT_BRANCH     master
)

FetchContent_MakeAvailable(fleetbattle)

if("${CMAKE_BUILD_TYPE}" MATCHES "Debug")
add_definitions(-DDEBUG)
endif()

include_directories(fleetbattle/include)

add_subdirectory(Catch2       ${CMAKE_BUILD_TYPE}/Catch2)
add_subdirectory(fleetBattle  ${CMAKE_BUILD_TYPE}/fleetBattle)
add_subdirectory(src          ${CMAKE_BUILD_TYPE}/Tests)
