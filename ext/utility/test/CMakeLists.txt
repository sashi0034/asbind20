include(GoogleTest)

add_executable(test_ext_math test_ext_math.cpp)
target_link_libraries(test_ext_math PRIVATE shared_test_lib)
gtest_discover_tests(test_ext_math)
if(EMSCRIPTEN)
    set_target_properties(test_ext_math PROPERTIES LINK_FLAGS "--preload-file ${CMAKE_CURRENT_SOURCE_DIR}/script/test_math.as@script/test_math.as")
    set_target_properties(test_ext_math PROPERTIES LINK_DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/script/test_math.as)
else()
    configure_file(script/test_math.as ${CMAKE_CURRENT_BINARY_DIR}/script/test_math.as COPYONLY)
endif()

add_executable(test_ext_weakref test_ext_weakref.cpp)
target_link_libraries(test_ext_weakref PRIVATE shared_test_lib)
gtest_discover_tests(test_ext_math)

add_subdirectory("test_ext_vocabulary")
