include_directories(
	${CMAKE_SOURCE_DIR}
	${CMAKE_SOURCE_DIR}/scribus
)

set(ODT_IM_PLUGIN_MOC_CLASSES
	odtdia.h
)

set(ODT_IM_PLUGIN_SOURCES
	contentreader.cpp
	odtdia.cpp
	odtim.cpp
	stylereader.cpp
)

set(SCRIBUS_ODT_IM_PLUGIN "odtimplugin")

QT5_WRAP_CPP(ODT_IM_PLUGIN_MOC_SOURCES ${ODT_IM_PLUGIN_MOC_CLASSES})

add_library(${SCRIBUS_ODT_IM_PLUGIN} MODULE ${ODT_IM_PLUGIN_SOURCES} ${ODT_IM_PLUGIN_MOC_SOURCES})

target_link_libraries(${SCRIBUS_ODT_IM_PLUGIN} ${PLUGIN_LIBRARIES})

if(WANT_PCH)
	target_precompile_headers(${SCRIBUS_ODT_IM_PLUGIN} PRIVATE "../../plugins_pch.h")
endif()

install(TARGETS ${SCRIBUS_ODT_IM_PLUGIN}
	LIBRARY
	DESTINATION ${PLUGINDIR}gettext
	PERMISSIONS ${PLUGIN_PERMISSIONS}
)

# set_target_properties(${SCRIBUS_FONTPREVIEW_PLUGIN} PROPERTIES VERSION "0.0.0")
