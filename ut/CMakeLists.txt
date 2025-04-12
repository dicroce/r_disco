
add_executable(
    r_disco_ut
    include/framework.h
    source/framework.cpp
    include/test_r_disco.h
    source/test_r_disco.cpp
)

if(MSVC)
    target_link_options(r_onvif_ut PUBLIC "/STACK:10000000")
endif()

target_include_directories(
    r_disco_ut PUBLIC 
    include
    ../include
    ${r_utils_SOURCE_DIR}/include
    ${r_onvif_SOURCE_DIR}/include
    ${r_db_SOURCE_DIR}/include
    ${r_pipeline_SOURCE_DIR}/include
)
target_link_libraries(
    r_disco_ut LINK_PUBLIC
    r_disco
    r_pipeline
    r_db
    r_onvif
    r_utils
)
