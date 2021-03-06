cmake_minimum_required(VERSION 3.2)
set(SOIL_TARGET soil)
project(${SOIL_TARGET})

set(INCLUDE_DIR "${PROJECT_SOURCE_DIR}/include")
set(
  INCLUDE_FILES
  "${INCLUDE_DIR}/SOIL/image_dxt.h" "${INCLUDE_DIR}/SOIL/image_helper.h"
  "${INCLUDE_DIR}/SOIL/SOIL.h" "${INCLUDE_DIR}/SOIL/stb_image_aug.h"
  "${INCLUDE_DIR}/SOIL/stbi_dds_aug_c.h" "${INCLUDE_DIR}/SOIL/stbi_dds_aug.h"
)

set(SRC_DIR "${PROJECT_SOURCE_DIR}/src")
set(
  SRC_FILES "${SRC_DIR}/image_dxt.c" "${SRC_DIR}/image_helper.c"
  "${SRC_DIR}/soil.c" "${SRC_DIR}/stb_image_aug.c"
)

if(BUILD_SHARED_LIBS)
  add_library(${SOIL_TARGET} SHARED)
else()
  add_library(${SOIL_TARGET} STATIC)
endif()

target_include_directories(
  ${SOIL_TARGET}
  PUBLIC ${INCLUDE_DIR} ${OPENGL_INCLUDE_DIR}
  PRIVATE "${INCLUDE_DIR}/SOIL"
)

target_sources(
  ${SOIL_TARGET}
  PUBLIC ${INCLUDE_FILES}
  PRIVATE ${SRC_FILES}
)

set(OpenGL_GL_PREFERENCE "GLVND")

find_package(OpenGL REQUIRED)
target_link_libraries(${SOIL_TARGET} ${OPENGL_LIBRARIES})
