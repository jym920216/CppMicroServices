
enable_language(C)

include_directories(../../third_party)

add_definitions(-DUS_RCC_EXECUTABLE_NAME=\"${US_RCC_EXECUTABLE_OUTPUT_NAME}\")

set(srcs ResourceCompiler.cpp ../../third_party/miniz.c ../../third_party/jsoncpp.cpp)

add_executable(${US_RCC_EXECUTABLE_TARGET} ${srcs})
set_property(TARGET ${US_RCC_EXECUTABLE_TARGET} PROPERTY OUTPUT_NAME ${US_RCC_EXECUTABLE_OUTPUT_NAME})
if(WIN32)
  target_link_libraries(${US_RCC_EXECUTABLE_TARGET} Shlwapi)
endif()

set_property(
  TARGET ${US_RCC_EXECUTABLE_TARGET} APPEND PROPERTY
  COMPILE_DEFINITIONS "MINIZ_NO_ARCHIVE_READING_API;MINIZ_NO_ZLIB_COMPATIBLE_NAMES"
  )

if(NOT US_NO_INSTALL)
  install(TARGETS ${US_RCC_EXECUTABLE_TARGET}
          EXPORT ${PROJECT_NAME}Targets
          FRAMEWORK DESTINATION . ${US_SDK_INSTALL_COMPONENT}
          RUNTIME DESTINATION bin ${US_SDK_INSTALL_COMPONENT})
endif()
