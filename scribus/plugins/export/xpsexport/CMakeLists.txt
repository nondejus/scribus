include_directories(
	${CMAKE_SOURCE_DIR}
	${CMAKE_SOURCE_DIR}/scribus
)

set(EXPORTXPS_PLUGIN_MOC_CLASSES
	xpsexplugin.h
)

set(EXPORTXPS_PLUGIN_SOURCES
	xpsexplugin.cpp
)

set(SCRIBUS_EXPORTXPS_PLUGIN "xpsexplugin")

QT5_WRAP_CPP(EXPORTXPS_PLUGIN_MOC_SOURCES ${EXPORTXPS_PLUGIN_MOC_CLASSES})

add_library(${SCRIBUS_EXPORTXPS_PLUGIN} MODULE ${EXPORTXPS_PLUGIN_SOURCES} ${EXPORTXPS_PLUGIN_MOC_SOURCES})

target_link_libraries(${SCRIBUS_EXPORTXPS_PLUGIN} ${PLUGIN_LIBRARIES} ${SCRIBUS_ZIP_LIB})

if(WANT_PCH)
	target_precompile_headers(${SCRIBUS_EXPORTXPS_PLUGIN} PRIVATE "../../plugins_pch.h")
endif()

install(TARGETS ${SCRIBUS_EXPORTXPS_PLUGIN}
	LIBRARY
	DESTINATION ${PLUGINDIR}
	PERMISSIONS ${PLUGIN_PERMISSIONS}
)

add_dependencies(${SCRIBUS_EXPORTXPS_PLUGIN} ${EXE_NAME})

# set_target_properties(${SCRIBUS_FONTPREVIEW_PLUGIN} PROPERTIES VERSION "0.0.0")
