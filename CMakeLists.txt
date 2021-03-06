cmake_minimum_required(VERSION 2.8.3)
project(Argos)
set_property(GLOBAL PROPERTY COMPILE_FLAGS "-m64")
set_property(GLOBAL PROPERTY LINK_FLAGS "-m64")
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)

set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/CMakeModules)

if(ARGOS_BUILD_STATIC)
    set(Boost_USE_STATIC_LIBS on)
    set(Boost_USE_STATIC_RUNTIME on)
    set(CMAKE_FIND_LIBRARY_SUFFIXES .a)
    set(BUILD_SHARED_LIBS OFF)
    set(CMAKE_EXE_LINKER_FLAGS "-static")    
endif() 

find_package(Boost 1.50.0 COMPONENTS system filesystem thread program_options regex iostreams REQUIRED)
find_package(ICU 4.8 REQUIRED data i18n uc)
find_package(Protobuf 2.4 REQUIRED)

INCLUDE_DIRECTORIES(
    ${Boost_INCLUDE_DIRS}
    ${ICU_INCLUDE_DIRS}
    ${PROTOBUF_INCLUDE_DIR}
    ${CMAKE_SOURCE_DIR}/include
    .
)

SET(LIBS_MISC)
LIST(APPEND LIBS_MISC ${Boost_LIBRARIES})
LIST(APPEND LIBS_MISC ${ICU_LIBRARIES})

ADD_SUBDIRECTORY(json_spirit)
ADD_SUBDIRECTORY(pugixml)
ADD_SUBDIRECTORY(common)
ADD_SUBDIRECTORY(index)
ADD_SUBDIRECTORY(query)
ADD_SUBDIRECTORY(parser)
ADD_SUBDIRECTORY(argos_ri_backend)
ADD_SUBDIRECTORY(serialization)
ADD_SUBDIRECTORY(net)
ADD_SUBDIRECTORY(analyzer)
ADD_SUBDIRECTORY(indexer)
ADD_SUBDIRECTORY(searcher)


