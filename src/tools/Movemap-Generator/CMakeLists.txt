#
# This code is part of MaNGOS. Contributor & Copyright details are in AUTHORS/THANKS.
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
#

cmake_minimum_required (VERSION 2.8)

project(mmap-generator)

set(EXECUTABLE_NAME mmap-generator)

if(debug)
    add_definitions(-DDEBUG)
endif()

# zlib
if(WIN32 AND MSVC)
    add_definitions(-DNO_vsnprintf)
endif()

include_directories(
    ${CMAKE_SOURCE_DIR}/src
    ${CMAKE_SOURCE_DIR}/src/shared
    ${CMAKE_SOURCE_DIR}/src/game
    ${CMAKE_SOURCE_DIR}/src/game/vmap
    ${CMAKE_SOURCE_DIR}/dep/include/g3dlite
    ${CMAKE_SOURCE_DIR}/dep/ACE_wrappers
    ${CMAKE_BINARY_DIR}/dep/ACE_wrappers
    ${CMAKE_SOURCE_DIR}/src/framework
    ${CMAKE_SOURCE_DIR}/dep/recastnavigation/Detour/Include
    ${CMAKE_SOURCE_DIR}/dep/recastnavigation/Recast/Include
    ${CMAKE_SOURCE_DIR}/dep/src/zlib
)

set(SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/IntermediateValues.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/generator.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/MapBuilder.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/TerrainBuilder.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/VMapExtensions.cpp
)

add_executable(${EXECUTABLE_NAME} ${SOURCES})

target_link_libraries(${EXECUTABLE_NAME} g3dlite vmap detour recast zlib shared)

install(TARGETS ${EXECUTABLE_NAME} DESTINATION ${BIN_DIR}/${TOOLS_DIR})
