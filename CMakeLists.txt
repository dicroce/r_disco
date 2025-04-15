cmake_minimum_required(VERSION 3.28.3)
set(PROJECT_VERSION_MAJOR 0)
set(PROJECT_VERSION_MINOR 0)
set(PROJECT_VERSION_PATCH 1)
project(r_disco VERSION ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH})

include(r_build.txt)
include(GSTREAMERConfig.cmake REQUIRED)
include(FetchContent)

FetchContent_Declare(
    r_utils
    GIT_REPOSITORY https://github.com/dicroce/r_utils.git
    GIT_TAG        main
    FIND_PACKAGE_ARGS NAMES r_utils
)
FetchContent_MakeAvailable(r_utils)

FetchContent_Declare(
    r_onvif
    GIT_REPOSITORY https://github.com/dicroce/r_onvif.git
    GIT_TAG        main
    FIND_PACKAGE_ARGS NAMES r_onvif
)
FetchContent_MakeAvailable(r_onvif)

FetchContent_Declare(
    r_db
    GIT_REPOSITORY https://github.com/dicroce/r_db.git
    GIT_TAG        main
    FIND_PACKAGE_ARGS NAMES r_db
)
FetchContent_MakeAvailable(r_db)

FetchContent_Declare(
    r_pipeline
    GIT_REPOSITORY https://github.com/dicroce/r_pipeline.git
    GIT_TAG        main
    FIND_PACKAGE_ARGS NAMES r_pipeline
)
FetchContent_MakeAvailable(r_pipeline)  

add_library(
    r_disco
    include/r_disco/providers/r_onvif_provider.h
    source/providers/r_onvif_provider.cpp
    include/r_disco/r_agent.h
    source/r_agent.cpp
    include/r_disco/r_camera.h
    include/r_disco/r_devices.h
    source/r_devices.cpp
    include/r_disco/r_stream_config.h
    source/r_stream_config.cpp
)

target_include_directories(
    r_disco PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

target_link_libraries(
    r_disco
    r_pipeline
    r_db
    r_onvif
    r_utils
    uuid
    ${GST_LIBS}
)

add_subdirectory(ut)

if(PROJECT_IS_TOP_LEVEL)
configure_dev_package("r_disco" "A C++ library that manages a collection of ONVIF cameras.")
endif()