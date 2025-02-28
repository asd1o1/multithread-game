macro(package_add_test TESTNAME)
    add_executable(${TESTNAME} ${ARGN})
    target_link_libraries(${TESTNAME} gtest gmock gtest_main)
    gtest_discover_tests(
        ${TESTNAME}
        WORKING_DIRECTORY ${PROJECT_DIR}
        PROPERTIES VS_DEBUGGER_WORKING_DIRECTORY "${PROJECT_DIR}"
    )
    set_target_properties(${TESTNAME} PROPERTIES FOLDER tests)
endmacro()

configure_file(pathTo.save pathTo.save COPYONLY)

package_add_test(board_test board_test.cpp ../src/board.cpp ../src/interface.cpp ../src/tile.cpp ../src/utility.cpp)
target_link_libraries(board_test cereal)

package_add_test(utility_test utility_test.cpp ../src/board.cpp ../src/tile.cpp ../src/utility.cpp)
target_link_libraries(utility_test cereal)