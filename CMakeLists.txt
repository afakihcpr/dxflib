cmake_minimum_required(VERSION 2.8.3)
project(dxflib)

find_package(catkin REQUIRED)

catkin_package(
   INCLUDE_DIRS include
   LIBRARIES ${PROJECT_NAME}
#  CATKIN_DEPENDS other_catkin_pkg
#  DEPENDS system_lib
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

###########
## Build ##
###########

add_library(${PROJECT_NAME}
   src/dl_dxf.cpp
   src/dl_writer_ascii.cpp
   include/dxflib/dl_attributes.h
   include/dxflib/dl_creationadapter.h
   include/dxflib/dl_entities.h
   include/dxflib/dl_extrusion.h
   include/dxflib/dl_writer.h
   include/dxflib/dl_codes.h
   include/dxflib/dl_creationinterface.h
   include/dxflib/dl_dxf.h
   include/dxflib/dl_exception.h
   include/dxflib/dl_global.h
   include/dxflib/dl_writer_ascii.h
)
add_dependencies(${PROJECT_NAME} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})

#############
## examples #
#############

add_executable(readwrite
   examples/readwrite/main.cpp
   examples/readwrite/test_creationclass.cpp
   examples/readwrite/test_creationclass.h
)
add_dependencies(readwrite ${catkin_EXPORTED_TARGETS})
target_link_libraries(readwrite ${PROJECT_NAME} ${catkin_LIBRARIES})

add_executable(writedimension
   examples/writedimension/main.cpp
)
add_dependencies(writedimension ${catkin_EXPORTED_TARGETS})
target_link_libraries(writedimension ${PROJECT_NAME} ${catkin_LIBRARIES})

add_executable(writehatch
   examples/writehatch/main.cpp
)
add_dependencies(writehatch ${catkin_EXPORTED_TARGETS})
target_link_libraries(writehatch ${PROJECT_NAME} ${catkin_LIBRARIES})

#############
## Install ##
#############

# Mark executables and/or libraries for installation
install(TARGETS ${PROJECT_NAME} readwrite writedimension writehatch
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

# Mark cpp header files for installation
install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
  PATTERN ".svn" EXCLUDE
)

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_dxflib.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
