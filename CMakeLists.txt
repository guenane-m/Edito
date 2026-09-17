cmake_minimum_required(VERSION 3.16)
project(Edito VERSION 1.0 LANGUAGES C CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOUIC ON)

find_package(Qt6 REQUIRED COMPONENTS Gui Widgets)

qt_standard_project_setup()

qt_add_executable(Edito WIN32 MACOSX_BUNDLE
    src/core/encdetector.cpp src/core/encdetector.h
    src/core/main.cpp
    src/core/spellchecker.cpp src/core/spellchecker.h
    src/dialogs/findandreplace.cpp src/dialogs/findandreplace.h src/dialogs/findandreplace.ui
    src/dialogs/gotodialog.cpp src/dialogs/gotodialog.h src/dialogs/gotodialog.ui
    src/dialogs/preferencesdialog.cpp src/dialogs/preferencesdialog.h src/dialogs/preferencesdialog.ui
    src/ui/codeeditor.cpp src/ui/codeeditor.h
    src/ui/edito.cpp src/ui/edito.h src/ui/edito.ui
    src/ui/editor.cpp src/ui/editor.h src/ui/editor.ui
    third-party/hunspell/affentry.cxx third-party/hunspell/affentry.hxx
    third-party/hunspell/affixmgr.cxx third-party/hunspell/affixmgr.hxx
    third-party/hunspell/atypes.hxx
    third-party/hunspell/baseaffix.hxx
    third-party/hunspell/csutil.cxx third-party/hunspell/csutil.hxx
    third-party/hunspell/filemgr.cxx third-party/hunspell/filemgr.hxx
    third-party/hunspell/hashmgr.cxx third-party/hunspell/hashmgr.hxx
    third-party/hunspell/htypes.hxx
    third-party/hunspell/hunspell.cxx third-party/hunspell/hunspell.h third-party/hunspell/hunspell.hxx
    third-party/hunspell/hunversion.h
    third-party/hunspell/hunvisapi.h
    third-party/hunspell/hunzip.cxx third-party/hunspell/hunzip.hxx
    third-party/hunspell/langnum.hxx
    third-party/hunspell/phonet.cxx third-party/hunspell/phonet.hxx
    third-party/hunspell/replist.cxx third-party/hunspell/replist.hxx
    third-party/hunspell/suggestmgr.cxx third-party/hunspell/suggestmgr.hxx
    third-party/hunspell/utf_info.hxx
    third-party/hunspell/w_char.hxx
)
target_include_directories(Edito PRIVATE
    src/core
    src/dialogs
    src/ui
    third-party/hunspell
    third-party/uchardet
)

target_compile_definitions(Edito PRIVATE
    HUNSPELL_STATIC
    PROJECT_ROOT=\"${CMAKE_CURRENT_SOURCE_DIR}/\"
)

target_link_directories(Edito PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/third-party/uchardet
)

target_link_libraries(Edito PRIVATE
    Qt::Core
    Qt::Gui
    Qt::Widgets
    uchardet
)


# Resources:
set(Resources_resource_files
    "icons/close.png"
    "icons/closeAll.png"
    "icons/copy.png"
    "icons/cut.png"
    "icons/delete.png"
    "icons/editoIco.png"
    "icons/exit.png"
    "icons/find.png"
    "icons/home.png"
    "icons/lower.png"
    "icons/match_case.png"
    "icons/match_word.png"
    "icons/new.png"
    "icons/noFile.png"
    "icons/notsaved.png"
    "icons/open.png"
    "icons/paste.png"
    "icons/preserve_case.png"
    "icons/redo.png"
    "icons/regular_expression.png"
    "icons/replace.png"
    "icons/replace_all.png"
    "icons/save.png"
    "icons/saveAll.png"
    "icons/saved.png"
    "icons/selectAll.png"
    "icons/selectLine.png"
    "icons/settings.png"
    "icons/undo.png"
    "icons/upper.png"
    "icons/web.png"
    "icons/zoomIn.png"
    "icons/zoomOut.png"
    "dictionaries/ar.aff"
    "dictionaries/ar.dic"
    "dictionaries/en_US.aff"
    "dictionaries/en_US.dic"
    "dictionaries/fr.aff"
    "dictionaries/fr.dic"
)

qt_add_resources(Edito "Resources"
    PREFIX
        "/"
    FILES
        ${Resources_resource_files}
)

install(TARGETS Edito
    BUNDLE DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

qt_generate_deploy_app_script(
    TARGET Edito
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})
