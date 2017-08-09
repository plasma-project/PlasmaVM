cmake_minimum_required(VERSION 3.8)
project(PlasmaVM)
file(GLOB SOURCE_FILES RELATIVE "src" "*.cpp")
file(GLOB HEADER_FILES RELATIVE "src" "*.h")
option(BUILD_DOC "Build documentation" ON)
find_package(Doxygen)
if (DOXYGEN_FOUND)
    set(DOXYGEN_IN ${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in)
    set(DOXYGEN_OUT ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile)
    configure_file(${DOXYGEN_IN} ${DOXYGEN_OUT})
    add_custom_target(docs ALL
            COMMAND ${DOXYGEN_EXECUTABLE} ${DOXYGEN_OUT}
            WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
            COMMENT "Generating API documentation with Doxygen"
            VERBATIM)
endif (DOXYGEN_FOUND)
add_executable(PlasmaVM main.cpp ${SOURCE_FILES} ${HEADER_FILES})