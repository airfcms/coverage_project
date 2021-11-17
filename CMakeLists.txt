cmake_minimum_required (VERSION 3.8)

#include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/cli ${CMAKE_CURRENT_SOURCE_DIR}/lib ${CMAKE_CURRENT_SOURCE_DIR}/package1 ${CMAKE_CURRENT_SOURCE_DIR}/package2) 

project (coverage_project) 

set(COVERAGE_PROJECT_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/src CACHE STRING "Project include dirs")

include_directories( ${COVERAGE_PROJECT_INCLUDE_DIRS}) 

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")

if(CMAKE_COMPILER_IS_GNUCXX)
    SET(CMAKE_CXX_FLAGS "-g -O0 -fprofile-arcs -ftest-coverage")
    #include(CodeCoverage)
endif()


file(GLOB coverage_project_SRCS
	"src/main.cc"
	"src/component1.cc"
)

set(COVERAGE_PROJECT_SOURCE_FILES ${coverage_project_SRCS} CACHE STRING "Project source files")

add_executable (coverage_project ${coverage_project_SRCS})

#add_subdirectory( ${CMAKE_CURRENT_SOURCE_DIR}/tests )
