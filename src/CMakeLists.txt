INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/../lib
  ${CMAKE_CURRENT_BINARY_DIR}/..)

CHECK_FUNCTION_EXISTS(getopt HAVE_GETOPT)
IF(NOT HAVE_GETOPT)
  SET(SRC_EXTRA_FILES getopt.c)
ENDIF(NOT HAVE_GETOPT)

ADD_EXECUTABLE(zipcmp zipcmp.c ${SRC_EXTRA_FILES})
TARGET_LINK_LIBRARIES(zipcmp zip)
INSTALL(TARGETS zipcmp RUNTIME DESTINATION bin)

ADD_EXECUTABLE(zipmerge zipmerge.c ${SRC_EXTRA_FILES})
TARGET_LINK_LIBRARIES(zipmerge zip)
INSTALL(TARGETS zipmerge RUNTIME DESTINATION bin)

ADD_EXECUTABLE(ziptool ziptool.c ${SRC_EXTRA_FILES} source_hole.c)
TARGET_LINK_LIBRARIES(ziptool zip)
INSTALL(TARGETS ziptool RUNTIME DESTINATION bin)

ADD_EXECUTABLE(hole hole.c ${SRC_EXTRA_FILES} source_hole.c)
TARGET_LINK_LIBRARIES(hole zip)
# do not install hole, just a test helper
