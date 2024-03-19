cmake_minimum_required(VERSION 3.16)
project(kf6-kio-ftps)

find_package(ECM 6.0.0 NO_MODULE)
set(CMAKE_MODULE_PATH ${ECM_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake )
set(REQUIRED_QT_VERSION "6.5.0")
set(KF_DEP_VERSION "6.0.0")

include(KDEInstallDirs)
include(KDECMakeSettings)
include(KDECompilerSettings)
include(FeatureSummary)

find_package(Qt6 ${REQUIRED_QT_VERSION} CONFIG REQUIRED Network Widgets)
find_package(KF6 ${KF_DEP_VERSION} COMPONENTS KIO CoreAddons WidgetsAddons)
find_package(KF6CoreAddons ${KF_DEP_VERSION} REQUIRED)
find_package(KF6I18n ${KF_DEP_VERSION} REQUIRED)
include_directories(${KF6_INCLUDE_DIRS})

feature_summary(WHAT REQUIRED_PACKAGES_NOT_FOUND FATAL_ON_MISSING_REQUIRED_PACKAGES)

configure_file(config-kioworker-ftps.h.in ${CMAKE_CURRENT_BINARY_DIR}/config-kioworker-ftps.h )
kcoreaddons_add_plugin(kio_ftps INSTALL_NAMESPACE "kf6/kio")
target_sources(kio_ftps PRIVATE
    ftps.cpp
)
target_link_libraries(kio_ftps Qt6::Network KF6::KIOCore KF6::I18n KF6::ConfigCore KF6::WidgetsAddons)
