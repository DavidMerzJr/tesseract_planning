find_package(tesseract_environment REQUIRED)

add_executable(${PROJECT_NAME}_freespace_manager_example freespace_manager_example.cpp)
target_link_libraries(${PROJECT_NAME}_freespace_manager_example console_bridge::console_bridge ${PROJECT_NAME} tesseract::tesseract_environment_core tesseract::tesseract_environment_ofkt tesseract::tesseract_command_language tesseract::tesseract_support ${CMAKE_THREAD_LIBS_INIT})
target_compile_options(${PROJECT_NAME}_freespace_manager_example PRIVATE ${TESSERACT_COMPILE_OPTIONS_PRIVATE} ${TESSERACT_COMPILE_OPTIONS_PUBLIC})
target_compile_definitions(${PROJECT_NAME}_freespace_manager_example PRIVATE ${TESSERACT_COMPILE_DEFINITIONS})
target_clang_tidy(${PROJECT_NAME}_freespace_manager_example ARGUMENTS ${TESSERACT_CLANG_TIDY_ARGS} ENABLE ${TESSERACT_ENABLE_CLANG_TIDY})
target_cxx_version(${PROJECT_NAME}_freespace_manager_example PRIVATE VERSION ${TESSERACT_CXX_VERSION})
target_include_directories(${PROJECT_NAME}_freespace_manager_example PRIVATE
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>")
target_include_directories(${PROJECT_NAME}_freespace_manager_example SYSTEM PRIVATE
    ${EIGEN3_INCLUDE_DIRS})
list(APPEND Examples ${PROJECT_NAME}_freespace_manager_example)

add_executable(${PROJECT_NAME}_raster_manager_example raster_manager_example.cpp)
target_link_libraries(${PROJECT_NAME}_raster_manager_example console_bridge::console_bridge ${PROJECT_NAME} tesseract::tesseract_environment_core tesseract::tesseract_environment_ofkt tesseract::tesseract_command_language tesseract::tesseract_support  ${CMAKE_THREAD_LIBS_INIT})
target_compile_options(${PROJECT_NAME}_raster_manager_example PRIVATE ${TESSERACT_COMPILE_OPTIONS_PRIVATE} ${TESSERACT_COMPILE_OPTIONS_PUBLIC})
target_compile_definitions(${PROJECT_NAME}_raster_manager_example PRIVATE ${TESSERACT_COMPILE_DEFINITIONS})
target_clang_tidy(${PROJECT_NAME}_raster_manager_example ARGUMENTS ${TESSERACT_CLANG_TIDY_ARGS} ENABLE ${TESSERACT_ENABLE_CLANG_TIDY})
target_cxx_version(${PROJECT_NAME}_raster_manager_example PRIVATE VERSION ${TESSERACT_CXX_VERSION})
target_include_directories(${PROJECT_NAME}_raster_manager_example PRIVATE
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>")
target_include_directories(${PROJECT_NAME}_raster_manager_example SYSTEM PRIVATE
    ${EIGEN3_INCLUDE_DIRS})
list(APPEND Examples ${PROJECT_NAME}_raster_manager_example)

if(NOT WIN32)
  add_executable(${PROJECT_NAME}_memory_usage_example memory_usage_example.cpp)
  target_link_libraries(${PROJECT_NAME}_memory_usage_example console_bridge::console_bridge ${PROJECT_NAME} tesseract::tesseract_environment_core tesseract::tesseract_environment_ofkt tesseract::tesseract_command_language tesseract::tesseract_support  ${CMAKE_THREAD_LIBS_INIT})
  target_compile_options(${PROJECT_NAME}_memory_usage_example PRIVATE ${TESSERACT_COMPILE_OPTIONS_PRIVATE} ${TESSERACT_COMPILE_OPTIONS_PUBLIC})
  target_compile_definitions(${PROJECT_NAME}_memory_usage_example PRIVATE ${TESSERACT_COMPILE_DEFINITIONS})
  target_clang_tidy(${PROJECT_NAME}_memory_usage_example ARGUMENTS ${TESSERACT_CLANG_TIDY_ARGS} ENABLE ${TESSERACT_ENABLE_CLANG_TIDY})
  target_cxx_version(${PROJECT_NAME}_memory_usage_example PRIVATE VERSION ${TESSERACT_CXX_VERSION})
  target_include_directories(${PROJECT_NAME}_memory_usage_example PRIVATE
      "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>")
  target_include_directories(${PROJECT_NAME}_memory_usage_example SYSTEM PRIVATE
      ${EIGEN3_INCLUDE_DIRS})
  list(APPEND Examples ${PROJECT_NAME}_memory_usage_example)
endif()

install(TARGETS ${Examples}
        EXPORT ${PROJECT_NAME}-targets
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)
