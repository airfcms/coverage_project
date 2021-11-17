#############
### TESTS ###
#############
cmake_minimum_required (VERSION 3.8)

#include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/cli ${CMAKE_CURRENT_SOURCE_DIR}/lib ${CMAKE_CURRENT_SOURCE_DIR}/package1 ${CMAKE_CURRENT_SOURCE_DIR}/package2) 

project (coverage_tests) 

# tests
enable_testing()

################################
# Unit Tests
################################

if(CMAKE_COMPILER_IS_GNUCXX)
    SET(CMAKE_CXX_FLAGS "-g -O0 -fprofile-arcs -ftest-coverage")
    setup_target_for_coverage_gcovr_xml(NAME codeCoverageAnalysis EXECUTABLE coverage_tests coverage)
endif()

# Add test cpp file
add_executable( coverage_tests unit_test.cc component1.cc)
#add_executable( coverage_project_tests unit_test.cc component1.cc)
# Link test executable against gtest & gtest_main
target_link_libraries(coverage_tests gcov)
#run tests~
message (">>>>> ${CMAKE_CURRENT_SOURCE_DIR}")
add_test( NAME codeCoverageIntegration COMMAND /usr/bin/gcovr --xml -r ${CMAKE_CURRENT_SOURCE_DIR}/.. --object-directory=${CMAKE_BINARY_DIR}/src -o ${CMAKE_BINARY_DIR}/integration-report.xml)
