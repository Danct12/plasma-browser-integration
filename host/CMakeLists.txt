add_definitions(-DTRANSLATION_DOMAIN=\"plasma-browser-integration-host\")

configure_file(config-host.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/config-host.h)

set(HOST_SOURCES main.cpp
                connection.cpp
                pluginmanager.cpp
                settings.cpp
                mprisplugin.cpp
                abstractbrowserplugin.cpp
                kdeconnectplugin.cpp
                downloadplugin.cpp
                downloadjob.cpp
                tabsrunnerplugin.cpp
                purposeplugin.cpp
                )

qt5_add_dbus_adaptor(HOST_SOURCES ../dbus/org.kde.plasma.browser_integration.TabsRunner.xml tabsrunnerplugin.h TabsRunnerPlugin)
qt5_add_dbus_adaptor(HOST_SOURCES ../dbus/org.kde.plasma.browser_integration.Settings.xml settings.h Settings)

qt5_add_dbus_adaptor(HOST_SOURCES ../dbus/org.mpris.MediaPlayer2.xml mprisplugin.h MPrisPlugin mprisroot MPrisRoot)
qt5_add_dbus_adaptor(HOST_SOURCES ../dbus/org.mpris.MediaPlayer2.Player.xml mprisplugin.h MPrisPlugin mprisplayer MPrisPlayer)

add_executable(plasma-browser-integration-host ${HOST_SOURCES})
target_link_libraries(
    plasma-browser-integration-host
    Qt5::DBus
    Qt5::Gui
    Qt5::Widgets
    KF5::Activities
    KF5::Crash
    KF5::I18n
    KF5::KIOCore
    KF5::PurposeWidgets
    KF5::FileMetaData
)

install(TARGETS plasma-browser-integration-host ${KDE_INSTALL_TARGETS_DEFAULT_ARGS})
