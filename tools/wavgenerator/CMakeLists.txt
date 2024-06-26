# Set multi-language TS files
set(TS_FILES ts/wavgenerator_zh_CN.ts)

# Set project sources
file(GLOB_RECURSE SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/src/*)

set(PROJECT_SOURCES
    ${SOURCES}
    ${TS_FILES}
    ${CMAKE_SOURCE_DIR}/res/resources.qrc
)

if(WIN32)
    configure_file(
        ${CMAKE_CURRENT_SOURCE_DIR}/res/resources_win.rc.in
        ${CMAKE_CURRENT_BINARY_DIR}/res/resources_win.rc
        @ONLY
    )
    list(APPEND
        PROJECT_SOURCES
        ${CMAKE_CURRENT_BINARY_DIR}/res/resources_win.rc
    )
endif(WIN32)

# Set Qt executables
qt_add_executable(wavgenerator
    MANUAL_FINALIZATION
    ${PROJECT_SOURCES}
)
qt_create_translation(QM_FILES ${CMAKE_CURRENT_SOURCE_DIR} ${TS_FILES})

# Link libraries
target_link_libraries(wavgenerator PRIVATE
    Qt${QT_VERSION_MAJOR}::Widgets
    ${LIBAVUTIL_PATH}
    ${LIBAVCODEC_PATH}
    ${LIBAVFORMAT_PATH}
    ${LIBAVFILTER_PATH}
    ${LIBSWRESAMPLE_PATH}
)

# MacOS settings for Qt < 6.1.0 (For Qt > 6.1.0 this is configured automatically)
if(${QT_VERSION} VERSION_LESS 6.1.0)
  set(BUNDLE_ID_OPTION MACOSX_BUNDLE_GUI_IDENTIFIER tech.izwb.AVPStudio.wavgenerator)
endif()

# Modify Qt executable properties
set_target_properties(wavgenerator PROPERTIES
    ${BUNDLE_ID_OPTION}
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

# Qt finalize executable
qt_finalize_executable(wavgenerator)
