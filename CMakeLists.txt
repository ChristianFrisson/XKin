cmake_minimum_required( VERSION 2.6 )
project( XKin )

set( VERSION 1.0.0 )
set( PACKAGE_NAME ${CMAKE_PROJECT_NAME} )

set( CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR} )
find_path(OpenCV_DIR NAMES opencv-config.cmake OpenCVConfig.cmake PATH_SUFFIXES lib/cmake lib)
find_package( OpenCV REQUIRED COMPONENTS core imgproc highgui )
find_package( fftw REQUIRED )
find_package( freenect REQUIRED )
MESSAGE("${FREENECT_INCLUDE_DIR}")
include_directories( ${FREENECT_INCLUDE_DIR} )

set( CMAKE_BUILD_TYPE Debug )
set( CMAKE_C_FLAGS_DEBUG "-g" )
set( CMAKE_C_FLAGS_RELEASE "-O3" )
set( CMAKE_C_FLAGS_RELWITHDEBINFO "-O2 -g" )

configure_file( "${PROJECT_SOURCE_DIR}/config.h.in" 
	        "${PROJECT_BINARY_DIR}/config.h" ) 

include_directories( "${PROJECT_BINARY_DIR}" )

add_subdirectory( lib )
add_subdirectory( tools )
add_subdirectory( demo )

