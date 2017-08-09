cmake_minimum_required(VERSION 3.8)
project(PlasmaVM)
# The sources
file(GLOB SOURCE_FILES RELATIVE "src" "*.cpp")
# The headers
file(GLOB HEADER_FILES RELATIVE "src" "*.h")
#[[Turning on documentation building]]
option(BUILD_DOC "Build documentation" ON)
# Getting the doxygen package
find_package(Doxygen)
# Doxygen found!!
if (DOXYGEN_FOUND)
    #[[Setting Doxygen variables : for input and for output]]
    set(DOXYGEN_IN ${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in)
    set(DOXYGEN_OUT ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile)
    #Configure them
    configure_file(${DOXYGEN_IN} ${DOXYGEN_OUT})
    #[[Adding a custom target to build documentation for all projects]]
    add_custom_target(docs ALL
            COMMAND ${DOXYGEN_EXECUTABLE} ${DOXYGEN_OUT}
            WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
            COMMENT "Generating API documentation with Doxygen"
            VERBATIM)
    # Doxygen not found :(
else (DOXYGEN_FOUND)
    # Fatal errror
    message(FATAL "Could not find Doxygen.")
endif (DOXYGEN_FOUND)
# Adding the sources configured earlier to the executable
add_executable(PlasmaVM main.cpp ${SOURCE_FILES} ${HEADER_FILES})