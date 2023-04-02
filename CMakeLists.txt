cmake_minimum_required(VERSION 3.16)

project(Chat-Example LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 REQUIRED COMPONENTS Core Gui Qml Quick Sql)

qt_add_executable(Chat-Example WIN32 MACOSX_BUNDLE
    main.cpp
    sqlcontactmodel.cpp sqlcontactmodel.h
    sqlconversationmodel.cpp sqlconversationmodel.h
)

target_link_libraries(Chat-Example PRIVATE
    Qt::Core
    Qt::Gui
    Qt::Qml
    Qt::Quick
    Qt::Sql
)

# Resources:
qt_add_qml_module(Chat-Example
    URI Chat-Example
    VERSION 1.0
    QML_FILES
        "+Material/ChatToolBar.qml"
        "ChatToolBar.qml"
        "ContactPage.qml"
        "ConversationPage.qml"
        "main.qml"
    RESOURCES
        "images/Albert_Einstein.png"
        "images/Albert_Einstein@2x.png"
        "images/Albert_Einstein@3x.png"
        "images/Albert_Einstein@4x.png"
        "images/Ernest_Hemingway.png"
        "images/Ernest_Hemingway@2x.png"
        "images/Ernest_Hemingway@3x.png"
        "images/Ernest_Hemingway@4x.png"
        "images/Hans_Gude.png"
        "images/Hans_Gude@2x.png"
        "images/Hans_Gude@3x.png"
        "images/Hans_Gude@4x.png"
)

qt6_add_resources(Chat-Example "conf"
    PREFIX
        "/"
    FILES
        "qtquickcontrols2.conf"
)

add_custom_target(android-related-files SOURCES "android/AndroidManifest.xml")

set_property(TARGET Chat-Example APPEND PROPERTY
    QT_ANDROID_PACKAGE_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/android
)

install(TARGETS Chat-Example
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)
