cmake_minimum_required(VERSION 3.13.4)
project(library-name VERSION 0.1)

set(CMAKE_C_STANDARD 99)
set(CMAKE_CXX_STANDARD 17)

add_library(library-name)

target_include_directories(library-name 
        PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc/lib.h>
        $<INSTALL_INTERFACE:include/lib.h>
        PRIVATE
        src)

target_sources(library-name
        PRIVATE
        inc/lib.h 
        src/lib.c
        )

add_subdirectory(test)

install(TARGETS library-name 
        EXPORT library-nameTargets
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin
        INCLUDES DESTINATION include
        )

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
        library-nameConfigVersion.cmake
        VERSION ${PACKAGE_VERSION}
        COMPATIBILITY AnyNewerVersion
)

install(EXPORT library-nameTargets
        FILE library-nameTargets.cmake
        NAMESPACE library-name::
        DESTINATION lib/cmake/library-name
        )
configure_file(library-name-config.cmake.in library-name-config.cmake @ONLY)
install(FILES "${CMAKE_CURRENT_BINARY_DIR}/library-name-config.cmake"
        "${CMAKE_CURRENT_BINARY_DIR}/library-nameConfigVersion.cmake"
        DESTINATION lib/cmake/library-name
        )

include(InstallRequiredSystemLibraries)

set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/README.md")
set(CPACK_PACKAGE_VERSION_MAJOR "${library-name_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${library-name_VERSION_MINOR}")
include(CPack)


