cmake_minimum_required(VERSION 3.14)
set(PROJECT_VERSION_MAJOR 0)
set(PROJECT_VERSION_MINOR 0)
set(PROJECT_VERSION_PATCH 1)
project(r_disco VERSION ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH})

include(r_build.txt)
include(FetchContent)

FetchContent_Declare(
    r_utils
    GIT_REPOSITORY https://github.com/dicroce/r_utils.git
    GIT_TAG        main
)
FetchContent_MakeAvailable(r_utils)

FetchContent_Declare(
    r_onvif
    GIT_REPOSITORY https://github.com/dicroce/r_onvif.git
    GIT_TAG        main
)
FetchContent_MakeAvailable(r_onvif)

FetchContent_Declare(
    r_db
    GIT_REPOSITORY https://github.com/dicroce/r_db.git
    GIT_TAG        main
)
FetchContent_MakeAvailable(r_db)

FetchContent_Declare(
    r_pipeline
    GIT_REPOSITORY https://github.com/dicroce/r_pipeline.git
    GIT_TAG        main
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
    include
    ${r_utils_SOURCE_DIR}/include
    ${r_onvif_SOURCE_DIR}/include
    ${r_db_SOURCE_DIR}/include
    ${r_pipeline_SOURCE_DIR}/include
)

target_link_libraries(
    r_disco
    r_pipeline
    r_db
    r_onvif
    r_utils
)
