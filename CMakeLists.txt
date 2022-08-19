cmake_minimum_required(VERSION 3.12)

project(
  half
  VERSION 2.2.0
)

include(GNUInstallDirs)

# Create the target:
add_library(half INTERFACE)
target_include_directories(half
        INTERFACE
        $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>)
target_compile_features(half INTERFACE cxx_std_11)

# Install the target:
install(TARGETS half
        EXPORT half
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})

install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/half
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

# Config and export:
include(CMakePackageConfigHelpers)
write_basic_package_version_file(
        ${CMAKE_CURRENT_BINARY_DIR}/halfConfigVersion.cmake
        VERSION ${PROJECT_VERSION}
        COMPATIBILITY SameMajorVersion)

install(EXPORT half
        FILE halfTargets.cmake
        NAMESPACE half::
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/half)

install(FILES
        ${PROJECT_SOURCE_DIR}/cmake/halfConfig.cmake
        ${CMAKE_CURRENT_BINARY_DIR}/halfConfigVersion.cmake
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/half)
