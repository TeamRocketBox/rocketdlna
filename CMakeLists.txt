# Copyright 2020 Christian Ege <ch@ege.io>
#
#  SPDX-License-Identifier: GPL-2.0-or-later
#
# This file is part of RocketDLNA.

cmake_minimum_required(VERSION 3.10.2)
project(rocketdlna VERSION 0.0.1 LANGUAGES CXX C )

set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake/modules")

# Variable definitions
set(TIVO_SUPPORT_ENABLED OFF  CACHE BOOL "TiVo Support")
set(ROOTDEV_MANUFACTURER_NAME "The Rocket Box Team" CACHE STRING "Manufacturer name")
set(ROOTDEV_MODELNAME "Windows Media Connect compatible (RocketDLNA)" CACHE STRING "The Model name")
set(ROOTDEV_MANUFACTURER_URL "http://github.com/TheTeamRocketBox" CACHE STRING "Manufacturer URL")
set(ROOTDEV_MODELURL "http://github.com/TheTeamRocketBox" CACHE STRING "Model URL")
set(ROOTDEV_MODELDESCRIPTION "RocketDLNA on ${CMAKE_SYSTEM_NAME}" CACHE STRING "The Model description")
set(ROCKETDLNA_DEFAULT_DB_PATH "/var/cache/rocketdlna"  CACHE STRING "Default path for the database" )
set(ROCKETDLNA_DEFAULT_LOG_PATH "/var/log" CACHE STRING "Default path for the log files")


add_subdirectory(src)
# Add support for the config header
include_directories("${CMAKE_CURRENT_BINARY_DIR}/src")

# specify the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64")

set(ROCKETDLNA_SOURCES minidlna.c
           upnphttp.c
           upnpdescgen.c
           upnpsoap.c
           upnpreplyparse.c
           minixml.c
           clients.c
           getifaddr.c
           process.c
           upnpglobalvars.c
           options.c
           minissdp.c
           uuid.c
           upnpevents.c
           sql.c utils.c
           metadata.c
           scanner.c
           monitor.c
           tivo_utils.c
           tivo_beacon.c
           tivo_commands.c
           playlist.c
           image_utils.c
           albumart.c
           log.c
           containers.c
           avahi.c
           tagutils/tagutils.c
           select.c
)

# Find the required libraries
find_package (JPEG REQUIRED)
find_package (SQLite3 REQUIRED)
find_package (Threads REQUIRED)
find_package (Flac REQUIRED)
find_package (Exif REQUIRED)
find_package (ID3Tag REQUIRED)
find_package (FFmpeg REQUIRED)
find_package (Ogg REQUIRED)
find_package (Vorbis REQUIRED)
find_package (Avahi REQUIRED)



add_executable(${PROJECT_NAME} ${ROCKETDLNA_SOURCES})
target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR} 
  ${EXIF_INCLUDE_DIRS}
  ${FFMPEG_INCLUDE_DIR}
  ${FLAC_INCLUDE_DIR}
)

target_link_libraries(${PROJECT_NAME}
  JPEG::JPEG
  SQLite::SQLite3
  Threads::Threads
  ${FLAC_LIBRARIES}
  ${EXIF_LIBRARIES}
  ${FFMPEG_LIBRARIES}
  Ogg::ogg
  Vorbis::vorbis
  ID3Tag::ID3Tag
  Avahi::Avahi
)

