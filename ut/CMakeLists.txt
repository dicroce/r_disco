
#find_package(PkgConfig)
#pkg_search_module(gstreamer REQUIRED IMPORTED_TARGET gstreamer-1.0)
#pkg_search_module(gstreamer-sdp REQUIRED IMPORTED_TARGET gstreamer-sdp-1.0)
#pkg_search_module(gstreamer-video REQUIRED IMPORTED_TARGET gstreamer-video-1.0)
#pkg_search_module(gstreamer-rtsp-server REQUIRED IMPORTED_TARGET gstreamer-rtsp-server-1.0)
#pkg_search_module(gstreamer-codecparsers REQUIRED IMPORTED_TARGET gstreamer-codecparsers-1.0)
##pkg_search_module(gstreamer-plugins-good REQUIRED IMPORTED_TARGET gstreamer-plugins-good-1.0)
#pkg_search_module(gstreamer-plugins-bad REQUIRED IMPORTED_TARGET gstreamer-plugins-bad-1.0)


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
 #   PkgConfig::gstreamer
 #   PkgConfig::gstreamer-sdp
 #   PkgConfig::gstreamer-app
 #   PkgConfig::gstreamer-video
)
target_link_directories(
    r_disco_ut PUBLIC
#    ${GST_LIBRARY_DIRS}
)
target_link_libraries(
    r_disco_ut LINK_PUBLIC
    r_disco
    r_pipeline
    r_db
    r_onvif
    r_utils
#    PkgConfig::gstreamer
#    PkgConfig::gstreamer-sdp
#    PkgConfig::gstreamer-app
#    PkgConfig::gstreamer-video
#    PkgConfig::gstreamer-rtsp-server
#    PkgConfig::gstreamer-codecparsers
#    PkgConfig::gstreamer-plugins-base
#    PkgConfig::gstreamer-plugins-good
#    PkgConfig::gstreamer-plugins-bad
)
