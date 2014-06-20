cmake_minimum_required(VERSION 2.8)

project(rtklib)

#set(CMAKE_POSITION_INDEPENDENT_CODE ON)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src/)

file(GLOB SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.c 
    ${CMAKE_CURRENT_SOURCE_DIR}/src/rcv/*.c
)

# Remove files that are causing errors
# Errors come form undefined symbols: set time, settspan, and showmsg
list(REMOVE_ITEM SOURCES
	${CMAKE_CURRENT_SOURCE_DIR}/src/convrnx.c  
	${CMAKE_CURRENT_SOURCE_DIR}/src/download.c 
	${CMAKE_CURRENT_SOURCE_DIR}/src/postpos.c)

#message(STATUS ${SOURCES})

add_library (core OBJECT ${SOURCES})

#add_library (${PROJECT_NAME} STATIC $<TARGET_OBJECTS:core>)
add_library (${PROJECT_NAME} SHARED $<TARGET_OBJECTS:core>)

## Install library and header files
install (FILES src/rtklib.h DESTINATION include/rtklib)
install (TARGETS ${PROJECT_NAME} DESTINATION lib)

