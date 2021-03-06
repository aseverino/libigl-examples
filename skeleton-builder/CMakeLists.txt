cmake_minimum_required(VERSION 2.8.6)

SET(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/../cmake)

# We need C++11. Put this directive after CGAL's include.
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -g -Wall -Wextra -Wno-reorder -Wno-unknown-pragmas -Wno-deprecated-declarations")
if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")
endif()

find_package(EIGEN REQUIRED)
include_directories( "${EIGEN_INCLUDE_DIR}" )
# Must be found before trying to find libraries in libigl/external
find_package(LIBIGL REQUIRED)
include_directories( "${LIBIGL_INCLUDE_DIR}" )
find_package(OpenGL REQUIRED)
find_package(GLUT REQUIRED)

link_directories(
  /usr/local/lib
  /opt/local/lib
  ${EIGEN_DIRS}
)

list(APPEND LIBS 
  ${LIBIGL_LIBRARIES} 
  ${OPENGL_LIBRARIES} 
  ${GLUT_LIBRARIES}
)

FILE(GLOB SRCFILES *.cpp)
add_executable(skeleton_builder ${SRCFILES})
target_link_libraries(skeleton_builder ${LIBS})
