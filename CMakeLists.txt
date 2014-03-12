CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

# see cmake --help-policy CMP0003 for more information
IF(COMMAND cmake_policy)
   CMAKE_POLICY(SET CMP0003 NEW)
ENDIF(COMMAND cmake_policy)


# Common to all platforms:
#SET(OSG_DIR "" CACHE PATH "set to base osg install path")
SET(DELTA3D_ROOT "" CACHE PATH "set to base osg install path")
SET(CMAKE_DEBUG_POSTFIX "d" CACHE STRING "add a postfix for Debug mode, usually d on windows")

#Convert to CMake standard path string
#FILE(TO_CMAKE_PATH "$ENV{DELTA_ROOT}" DELTA_ROOT_CMAKE)
#SET(DELTA3D_SOURCE_DIR "")

#SET(CMAKE_MODULE_PATH ${DELTA3D_SOURCE_DIR}/CMakeModules) #where the Find*.cmake files are
# We have some custom .cmake scripts not in the official distribution.
# Maybe this can be used override existing behavior if needed?
#SET(CMAKE_MODULE_PATH "${DELTA3D_SOURCE_DIR}/CMakeModules;${CMAKE_MODULE_PATH}") #where the Find*.cmake files are
#FILE(TO_NATIVE_PATH "$ENV{DELTA_ROOT}" DELTA_ROOT_CMAKE)

SET(CMAKE_MODULE_PATH "${DELTA3D_ROOT}/CMakeModules;${CMAKE_MODULE_PATH}") #where the Find*.cmake files are

PROJECT(MyDeltaApp)

#FINDING THE DELTA3D LIBRARIES

FIND_PACKAGE(dtABC REQUIRED)
FIND_PACKAGE(dtCore REQUIRED)
FIND_PACKAGE(dtDAL REQUIRED)
FIND_PACKAGE(dtGame REQUIRED)
FIND_PACKAGE(dtUtil REQUIRED)

#ADDING THE INCLUDE DIRECTORIES
INCLUDE_DIRECTORIES(${DTABC_INCLUDE_DIRECTORIES}
                    ${DTCORE_INCLUDE_DIRECTORIES}
                    ${DTDAL_INCLUDE_DIRECTORIES}
                    ${DTGAME_INCLUDE_DIRECTORIES}
                    ${DTUTIL_INCLUDE_DIRECTORIES}
                   )
ADD_EXECUTABLE(MyDeltaApp main.cpp)
#LINKING WITH DELTA3D LIBRARIES
TARGET_LINK_LIBRARIES(MyDeltaApp ${DTABC_LIBRARIES}
                              ${DTCORE_LIBRARIES}
                              ${DTDAL_LIBRARIES}
                              ${DTGAME_LIBRARIES}
                              ${DTUTIL_LIBRARIES}
                      )
					  
					  