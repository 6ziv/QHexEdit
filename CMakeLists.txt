cmake_minimum_required(VERSION 3.20)
project(QHexEdit CXX)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
find_package(QT NAMES Qt6 Qt5 COMPONENTS Core Widgets Gui REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Core Widgets Gui REQUIRED)

set(PROJECT_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/document/commands/hexcommand.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/document/commands/insertcommand.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/document/commands/removecommand.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/document/commands/replacecommand.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/document/gapbuffer.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/document/qhexcursor.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/document/qhexdocument.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/document/qhextheme.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/paint/qhexmetrics.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/paint/qhexpainter.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/qhexedit.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/qhexeditprivate.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/document/metadata/qhexmetadataitem.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/document/metadata/qhexmetadata.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/document/commands/hexcommand.h
    ${CMAKE_CURRENT_SOURCE_DIR}/document/commands/insertcommand.h
    ${CMAKE_CURRENT_SOURCE_DIR}/document/commands/removecommand.h
    ${CMAKE_CURRENT_SOURCE_DIR}/document/commands/replacecommand.h
    ${CMAKE_CURRENT_SOURCE_DIR}/document/gapbuffer.h
    ${CMAKE_CURRENT_SOURCE_DIR}/document/qhexcursor.h
    ${CMAKE_CURRENT_SOURCE_DIR}/document/qhexdocument.h
    ${CMAKE_CURRENT_SOURCE_DIR}/document/qhextheme.h
    ${CMAKE_CURRENT_SOURCE_DIR}/paint/qhexmetrics.h
    ${CMAKE_CURRENT_SOURCE_DIR}/paint/qhexpainter.h
    ${CMAKE_CURRENT_SOURCE_DIR}/qhexedit.h
    ${CMAKE_CURRENT_SOURCE_DIR}/qhexeditprivate.h
    ${CMAKE_CURRENT_SOURCE_DIR}/document/metadata/qhexmetadataitem.h
    ${CMAKE_CURRENT_SOURCE_DIR}/document/metadata/qhexmetadata.h
    )
if(${QT_VERSION_MAJOR} GREATER_EQUAL 6)
    qt_add_library(QHexEdit
        STATIC
        MANUAL_FINALIZATION
        ${PROJECT_SOURCES}
    )
else()
    add_library(QHexEdit${PROJECT_SOURCES})
endif()
target_include_directories(QHexEdit SYSTEM
        PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}
        PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/paint
        PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/document
        PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/document/commands
        PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/document/metadata
)

target_link_libraries(QHexEdit PUBLIC Qt${QT_VERSION_MAJOR}::Core Qt${QT_VERSION_MAJOR}::Widgets  Qt${QT_VERSION_MAJOR}::Gui)
if(QT_VERSION_MAJOR EQUAL 6)
    qt_finalize_target(QHexEdit)
endif()
