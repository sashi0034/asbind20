find_package(Doxygen REQUIRED)
find_package(Sphinx REQUIRED)

file(GLOB_RECURSE documented_headers "${CMAKE_SOURCE_DIR}/include/*.hpp")

# Generate documents using Doxygen and Sphinx
add_custom_target(
    asbind20_doc
    COMMAND ${CMAKE_COMMAND} -E make_directory "${CMAKE_BINARY_DIR}/doxygen-output"
    COMMAND ${DOXYGEN_EXECUTABLE} "${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile"
    WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
    DEPENDS ${documented_headers} "${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile"
)

add_custom_target(
    asbind20_sphinx
    COMMAND ${SPHINX_EXECUTABLE} -b html "${CMAKE_CURRENT_SOURCE_DIR}" "${CMAKE_BINARY_DIR}/sphinx-output"
    DEPENDS asbind20_doc
    WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
)

