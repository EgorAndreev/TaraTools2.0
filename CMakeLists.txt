cmake_minimum_required (VERSION 3.16)
set(PROJ_NAME TaraTools2.0)
project (${PROJ_NAME})
file(GLOB_RECURSE SRC
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.hpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp"
)
IF (WIN32)
  add_executable(${PROJ_NAME} WIN32 ${SRC})
  add_custom_command(TARGET ${PROJ_NAME} POST_BUILD
  COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_RUNTIME_DLLS:${PROJ_NAME}> $<TARGET_FILE_DIR:${PROJ_NAME}>
  COMMAND_EXPAND_LISTS
  )

ELSE()
  #add_executable(${PROJ_NAME} ${SRC})
ENDIF()

target_include_directories(${PROJ_NAME} PUBLIC src)
add_subdirectory(external/wxWidgets)
target_link_libraries(${PROJ_NAME} wx::gl wx::net wx::core wx::base)