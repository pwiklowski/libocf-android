cmake_minimum_required(VERSION 3.4.1)

set(CMAKE_VERBOSE_MAKEFILE on)


#Clone those dependencies and put path to LIB_PATH variable
#git clone https://github.com/pwiklowski/liboic
#git clone https://github.com/pwiklowski/libcoap
#git clone https://github.com/pwiklowski/lightstdlib
set(LIB_PATH !FILLME!)


#libcoap
aux_source_directory(${LIB_PATH}/libcoap/ SRC_LIST)
INCLUDE_DIRECTORIES(${LIB_PATH}/std/)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Werror=sign-compare")
add_library(coap SHARED ${SRC_LIST})


#liboic
aux_source_directory(${LIB_PATH}/liboic/ SRC_LIST)
INCLUDE_DIRECTORIES(${LIB_PATH}/libcoap/)
INCLUDE_DIRECTORIES(${LIB_PATH}/std/)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Werror=sign-compare")
add_library(oic SHARED ${SRC_LIST})



INCLUDE_DIRECTORIES(${LIB_PATH}/liboic/)
INCLUDE_DIRECTORIES(${LIB_PATH}/libcoap/)
INCLUDE_DIRECTORIES(${LIB_PATH}/std/)

add_library(ocfapp SHARED ocfapp.cpp )

find_library(log-lib log)

target_link_libraries(ocfapp coap)
target_link_libraries(ocfapp oic)
target_link_libraries(ocfapp ${log-lib})
