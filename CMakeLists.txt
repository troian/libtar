cmake_minimum_required(VERSION 3.5)

project(tar LANGUAGES C)

set(
	SOURCES

    lib/append.c
    lib/block.c
    lib/decode.c
    lib/encode.c
    lib/extract.c
    lib/handle.c
    libtar/libtar.c
    lib/output.c
    lib/util.c
    lib/wrapper.c
    listhash/libtar_hash.c
	listhash/libtar_list.c
	listhash/libtar_listhash.h

    lib/libtar.h
    config.h

	compat/basename.c
	compat/compat.h
	compat/dirname.c
	compat/fnmatch.c
	compat/gethostbyname_r.c
	compat/gethostname.c
	compat/getservbyname_r.c
	compat/glob.c
	compat/inet_aton.c
	compat/snprintf.c
	compat/strdup.c
	compat/strlcat.c
	compat/strmode.c
	compat/strrstr.c
	compat/strsep.c
)


set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Os -s")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-unused-parameter")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-return-type")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-sign-compare")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-implicit-function-declaration")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-format")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-unused-but-set-variable")

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/listhash)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/lib)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/compat)
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_definitions("-DNEED_GLOB")
add_library(tar STATIC ${SOURCES})

target_include_directories(
	tar PUBLIC libtar
)
