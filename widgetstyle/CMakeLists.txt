cmake_minimum_required(VERSION 3.5)
project(odysseusstyle)

set(TARGET odysseusstyle)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_AUTOMOC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package(ECM REQUIRED NO_MODULE)
set(CMAKE_MODULE_PATH ${ECM_MODULE_PATH} ${ECM_KDE_MODULE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

set(QT Core Gui Widgets DBus)
find_package(Qt5 REQUIRED ${QT})
find_package(PkgConfig REQUIRED)
find_package(KF5 REQUIRED WindowSystem)

include(ECMQueryQmake)

set (SRCS
    blurhelper.cpp
    blurhelper.h
    pstyleplugin.cpp
    pstyleplugin.h
    basestyle.h
    basestyle.cpp
    phantomcolor.h
    phantomcolor.cpp
    shadowhelper.h
    shadowhelper.cpp
    tileset.h
    tileset.cpp
    boxshadowrenderer.h
    boxshadowrenderer.cpp
)

add_library(${TARGET} MODULE ${SRCS})
target_link_libraries(${TARGET}
    Qt5::GuiPrivate
    Qt5::Core
    Qt5::Gui
    Qt5::Widgets
    Qt5::DBus
    KF5::WindowSystem
    )

query_qmake(CMAKE_INSTALL_QTPLUGINDIR QT_INSTALL_PLUGINS)

install(TARGETS ${TARGET} DESTINATION ${CMAKE_INSTALL_QTPLUGINDIR}/styles/)
