project(liblatte)
cmake_minimum_required(VERSION 3.0 FATAL_ERROR)

set(CMAKE_CXX_STANDARD 14)
set(VERSION 0.3)
set(AUTHOR "Michail Vourlakos")
set(EMAIL "mvourlakos@gmail.com")
set(WEBSITE "https://userbase.kde.org/LatteDock")
set(BUG_ADDRESS "https://bugs.kde.org/enter_bug.cgi?product=lattedock")
set(FAQS "https://userbase.kde.org/LatteDock/FAQ")

set(QT_MIN_VERSION "5.9.0")
set(KF5_MIN_VERSION "5.38.0")

set(KF5_LOCALE_PREFIX "")

find_package(ECM ${KF5_MIN_VER} REQUIRED NO_MODULE)
set(CMAKE_MODULE_PATH ${ECM_MODULE_PATH} ${ECM_KDE_MODULE_DIR})

find_package(Qt5 ${QT_MIN_VERSION} CONFIG REQUIRED NO_MODULE COMPONENTS Qml Quick)

find_package(KF5 ${KF5_MIN_VERSION} REQUIRED COMPONENTS
    Declarative I18n Plasma PlasmaQuick)
    
include(ECMQMLModules)
ecm_find_qmlmodule(QtQuick 2.7)

include(CMakePackageConfigHelpers)
include(ECMGenerateExportHeader)
include(ECMGenerateHeaders)
include(ECMOptionalAddSubdirectory)
include(KDECMakeSettings)
include(KDECompilerSettings NO_POLICY_SCOPE)
include(KDEInstallDirs)

string(REPLACE "-Wall" "" CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS})
string(REPLACE "-Wformat-security" "" CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS})

message(STATUS "COMPILER FLAGS : ${CMAKE_CXX_FLAGS}")

add_subdirectory(src)
