cmake_minimum_required(VERSION 2.8)
project(double-conversion)

# pick a version #
set(double-conversion_VERSION 2.0.1)
set(double-conversion_SOVERSION_MAJOR 1)
set(double-conversion_SOVERSION_MINOR 0)
set(double-conversion_SOVERSION_PATCH 0)
set(double-conversion_SOVERSION
  ${double-conversion_SOVERSION_MAJOR}.${double-conversion_SOVERSION_MINOR}.${double-conversion_SOVERSION_PATCH})

#
# set up include dirs
include_directories("${PROJECT_SOURCE_DIR}"
  "${PROJECT_BINARY_DIR}"
  )

# Add src subdirectory
add_subdirectory(double-conversion)

#
# set up testing if requested
option(BUILD_TESTING "Build test programs" OFF)
if(BUILD_TESTING)
  enable_testing()
  include(CTest)
  add_subdirectory(test)
endif()

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  "${CMAKE_CURRENT_BINARY_DIR}/double-conversion/double-conversionConfigVersion.cmake"
  VERSION ${double-conversion_VERSION}
  COMPATIBILITY AnyNewerVersion)

export(EXPORT double-conversion-targets
  FILE "${CMAKE_CURRENT_BINARY_DIR}/double-conversion/double-conversionTargets.cmake")
configure_file(double-conversionConfig.cmake
  "${CMAKE_CURRENT_BINARY_DIR}/double-conversion/double-conversionConfig.cmake"
  COPYONLY)

install(EXPORT double-conversion-targets
  FILE double-conversionTargets.cmake
  DESTINATION lib/double-conversion/cmake)
install(
  FILES
    double-conversionConfig.cmake
    "${CMAKE_CURRENT_BINARY_DIR}/double-conversion/double-conversionConfigVersion.cmake"
  DESTINATION lib/double-conversion/cmake
  COMPONENT Devel)

