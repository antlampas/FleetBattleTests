#FALP Fleet Battle Tests © 2023-2024 by Antlampas is licensed under CC BY-SA 4.0. To view a copy of this license, visit http://creativecommons.org/licenses/by-sa/4.0/

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

string(TOLOWER "${UNITS}" UNITS)

string(FIND "${UNITS}" "agent"         AGENT         )
string(FIND "${UNITS}" "board"         BOARD         )
string(FIND "${UNITS}" "game"          GAME          )
string(FIND "${UNITS}" "matchmaster"   MATCHMASTER   )
string(FIND "${UNITS}" "opponentboard" OPPONENTBOARD )
string(FIND "${UNITS}" "player"        PLAYER        )
string(FIND "${UNITS}" "playerboard"   PLAYERBOARD   )
string(FIND "${UNITS}" "ships"         SHIPS         )
string(FIND "${UNITS}" "utilities"     UTILITIES     )

if(AGENT GREATER -1)
  message("Testing agent")
  add_definitions(-DTESTAGENT)
endif(AGENT GREATER -1)
if(BOARD GREATER -1)
  message("Testing board")
  add_definitions(-DTESTBOARD)
endif(BOARD GREATER -1)
if(GAME GREATER -1)
  message("Testing game")
  add_definitions(-DTESTGAME)
endif(GAME GREATER -1)
if(MATCHMASTER GREATER -1)
  message("Testing match master")
  add_definitions(-DTESTMATCHMASTER)
endif(MATCHMASTER GREATER -1)
if(OPPONENTBOARD GREATER -1)
  message("Testing oppoenent board")
  add_definitions(-DTESTOPPONENTBOARD)
endif(OPPONENTBOARD GREATER -1)
if(PLAYER GREATER -1)
  message("Testing player")
  add_definitions(-DTESTPLAYER)
endif(PLAYER GREATER -1)
if(PLAYERBOARD GREATER -1)
  message("Testing player board")
  add_definitions(-DTESTPLAYERBOARD)
endif(PLAYERBOARD GREATER -1)
if(SHIPS GREATER -1)
  message("Testing ships")
  add_definitions(-DTESTSHIPS)
endif(SHIPS GREATER -1)
if(UTILITIES GREATER -1)
  message("Testing utilities")
  add_definitions(-DTESTUTILITIES)
endif(UTILITIES GREATER -1)

include_directories(${CMAKE_CURRENT_BINARY_DIR}/_deps/fleetbattle-src/include)

add_subdirectory(src          ${CMAKE_BUILD_TYPE}/Tests)
