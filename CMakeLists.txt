project(pcro)

find_package(Qt4 4.6.0 REQUIRED)
find_package(OpenCV REQUIRED)
find_package(KDE4 REQUIRED)

link_directories(/usr/local/lib)

include_directories(/usr/include/sphinxbase)
include_directories(/usr/local/include/pocketsphinx)
set(pcro_SRS    alsasoundcard.cpp
                main.cpp
                mainwindow.cpp
                qcustomplot.cpp
                voicerecognition.cpp
                livevideo.cpp
                           
                alsasoundcard.h
                mainwindow.h
                qcustomplot.h
                ui_mainwindow.h
                voicerecognition.h
                livevideo.h
                )

INCLUDE(${QT_USE_FILE})

INCLUDE_DIRECTORIES(${QDBUS_INCLUDE_DIRS}
                    ${KDE4_INCLUDES}
                    ${OpenCV_INCLUDE_DIRS}
                    ${CMAKE_CURRENT_SOURCE_DIR}/opentld/3rdparty/cvblobs
                    ${CMAKE_CURRENT_SOURCE_DIR}/opentld/libopentld/imacq
                    ${CMAKE_CURRENT_SOURCE_DIR}/opentld/libopentld/mftracker
                    ${CMAKE_CURRENT_SOURCE_DIR}/opentld/libopentld/tld
                    ${CMAKE_CURRENT_SOURCE_DIR}/opentld/opentld/main
                    ${CMAKE_CURRENT_SOURCE_DIR}/tldinterface
                    ${OpenCV_INCLUDE_DIRS}
                    )
                    
#start OpenTLD

SUBDIRS(opentld/3rdparty/cvblobs)
SUBDIRS(opentld/libopentld)
SUBDIRS(opentld/opentld)
SUBDIRS(tldinterface)

#end OpenTLD

ADD_DEFINITIONS(${KDE4_ENABLE_EXCEPTIONS})
ADD_DEFINITIONS(${QT_DEFINITIONS})

KDE4_ADD_UI_FILES(pcro_SRS mainwindow.ui)

KDE4_ADD_EXECUTABLE(pcro ${pcro_SRS})

target_link_libraries(pcro    ${KDE4_KDECORE_LIBS}
                              ${KDE4_KDEUI_LIBS}
                              ${QT_QTCORE_LIBRARY}
                              ${QT_QTGUI_LIBRARY}
                              asound
                              sphinxbase
                              pocketsphinx
                              sphinxad
                              
                              tldinterface
                              main
                              libopentld
                              cvblobs
                              sqlite3
                              QtSql
                              )
INSTALL(FILES ${CMAKE_CURRENT_SOURCE_DIR}/mylm.lm
              ${CMAKE_CURRENT_SOURCE_DIR}/mydict.dic
        DESTINATION ~/.kde4/share/apps/voicerecognition/)
