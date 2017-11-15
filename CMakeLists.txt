CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

PROJECT(httpry)

option(C++11_ENABLE "C++11_ENABLE" OFF)

SET(CMAKE_C_COMPILER "/usr/bin/gcc")
SET(CMAKE_CXX_COMPILER "/usr/bin/c++")

IF(C++11_ENABLE)
    IF(APPLE)
    ELSEIF(UNIX)
        SET(CMAKE_C_COMPILER "/opt/rh/devtoolset-2/root/usr/bin/gcc")
        SET(CMAKE_CXX_COMPILER "/opt/rh/devtoolset-2/root/usr/bin/c++")
    ENDIF()
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 ")
ELSE()
    IF(APPLE)
    ELSEIF(UNIX)
        SET(CMAKE_C_COMPILER "/usr/bin/gcc")
        SET(CMAKE_CXX_COMPILER "/usr/bin/c++")
    ENDIF()
ENDIF()

MESSAGE("CMAKE_CXX_COMPILER: ${CMAKE_CXX_COMPILER}")

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2 -g -gstabs -Wall -funroll-loops")
SET(TARGET "httpry")
#SET(LIBRARY_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/lib)
SET(EXECUTABLE_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/bin)

AUX_SOURCE_DIRECTORY(src SOURCE_DIRS_SRC)

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/../../../c++/include)
INCLUDE_DIRECTORIES(/usr/include/pcap)
INCLUDE_DIRECTORIES(/usr/local/include/pcap)

#LINK_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/../../../c++/lib/release_linux/libUtils)
#LINK_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/../../../c++/lib/release_linux/libBase)

ADD_EXECUTABLE(${TARGET} ${SOURCE_DIRS_SRC})

TARGET_LINK_LIBRARIES(${TARGET} -lpcap -lm -lpthread -lstdc++)