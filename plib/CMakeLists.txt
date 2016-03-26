PROJECT(plib CXX)

SET(FNT_PUBLIC_HEADERS
	${PLIB_SOURCE_DIR}/src/fnt/fnt.h
)
SET(FNT_PRIVATE_HEADERS
	${PLIB_SOURCE_DIR}/src/fnt/fntLocal.h
)
SET(FNT_SRCS
	${PLIB_SOURCE_DIR}/src/fnt/fnt.cxx
	${PLIB_SOURCE_DIR}/src/fnt/fntBitmap.cxx
	${PLIB_SOURCE_DIR}/src/fnt/fntTXF.cxx
)

SET(JS_PUBLIC_HEADERS

	${PLIB_SOURCE_DIR}/src/js/js.h
)

SET(JS_SRCS
		${PLIB_SOURCE_DIR}/src/js/jsWindows.cxx
)

SET(UL_PUBLIC_HEADERS
	${PLIB_SOURCE_DIR}/src/util/ul.h
  ${PLIB_SOURCE_DIR}/src/util/ulRTTI.h
)

SET(UL_PRIVATE_HEADERS
	${PLIB_SOURCE_DIR}/src/util/ulLocal.h
)

SET(SG_SRCS
	${PLIB_SOURCE_DIR}/src/sg/sg.cxx
	${PLIB_SOURCE_DIR}/src/sg/sgd.cxx
)

SET(SG_PUBLIC_HEADERS
	${PLIB_SOURCE_DIR}/src/sg/sg.h
)

SET(SG_PRIVATE_HEADERS
)

SET(UL_SRCS
	${PLIB_SOURCE_DIR}/src/util/ul.cxx
	${PLIB_SOURCE_DIR}/src/util/ulClock.cxx
	${PLIB_SOURCE_DIR}/src/util/ulError.cxx
	${PLIB_SOURCE_DIR}/src/util/ulLinkedList.cxx
	${PLIB_SOURCE_DIR}/src/util/ulList.cxx
	${PLIB_SOURCE_DIR}/src/util/ulRTTI.cxx
)

SET(PUI_SRCS
	${PLIB_SOURCE_DIR}/src/pui/pu.cxx
	${PLIB_SOURCE_DIR}/src/pui/puArrowButton.cxx
	${PLIB_SOURCE_DIR}/src/pui/puBox.cxx
	${PLIB_SOURCE_DIR}/src/pui/puButton.cxx
	${PLIB_SOURCE_DIR}/src/pui/puButtonBox.cxx
	${PLIB_SOURCE_DIR}/src/pui/puDial.cxx
	${PLIB_SOURCE_DIR}/src/pui/puDialogBox.cxx
	${PLIB_SOURCE_DIR}/src/pui/puFont.cxx
	${PLIB_SOURCE_DIR}/src/pui/puFrame.cxx
	${PLIB_SOURCE_DIR}/src/pui/puGroup.cxx
	${PLIB_SOURCE_DIR}/src/pui/puInput.cxx
	${PLIB_SOURCE_DIR}/src/pui/puInputBase.cxx
	${PLIB_SOURCE_DIR}/src/pui/puInterface.cxx
	${PLIB_SOURCE_DIR}/src/pui/puListBox.cxx
	${PLIB_SOURCE_DIR}/src/pui/puMenuBar.cxx
	${PLIB_SOURCE_DIR}/src/pui/puObject.cxx
	${PLIB_SOURCE_DIR}/src/pui/puOneShot.cxx
	${PLIB_SOURCE_DIR}/src/pui/puPopup.cxx
	${PLIB_SOURCE_DIR}/src/pui/puPopupMenu.cxx
	${PLIB_SOURCE_DIR}/src/pui/puRange.cxx
	${PLIB_SOURCE_DIR}/src/pui/puSlider.cxx
	${PLIB_SOURCE_DIR}/src/pui/puText.cxx
	${PLIB_SOURCE_DIR}/src/pui/puValue.cxx
)

SET(PUI_PUBLIC_HEADERS
	${PLIB_SOURCE_DIR}/src/pui/pu.h
)

SET(PUI_PRIVATE_HEADERS
	${PLIB_SOURCE_DIR}/src/pui/puLocal.h
)

SET(PUAUX_SRCS
	${PLIB_SOURCE_DIR}/src/puAux/puAux.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxBiSlider.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxBiSliderWithEnds.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxChooser.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxComboBox.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxCompass.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxFileSelector.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxLargeInput.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxList.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxScrollBar.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxSelectBox.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxSliderWithInput.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxSpinBox.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxTriSlider.cxx
	${PLIB_SOURCE_DIR}/src/puAux/puAuxVerticalMenu.cxx
)

SET(PUAUX_PUBLIC_HEADERS
	${PLIB_SOURCE_DIR}/src/puAux/puAux.h
)

SET(PUAUX_PRIVATE_HEADERS
	${PLIB_SOURCE_DIR}/src/puAux/puAuxLocal.h
)

# Dependent include files
INCLUDE_DIRECTORIES(${PLIB_SOURCE_DIR}/src
	${PLIB_SOURCE_DIR}/src/util
	${CMAKE_CURRENT_BINARY_DIR})

IF(MSVC)
	ADD_DEFINITIONS(-D_CRT_SECURE_NO_WARNINGS)
	SET(CMAKE_DEBUG_POSTFIX "d")
ENDIF(MSVC)

IF(MINGW)
	SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -w")
ENDIF(MINGW)

ADD_LIBRARY(sg STATIC ${SG_SRCS} ${SG_PUBLIC_HEADERS})
TARGET_INCLUDE_DIRECTORIES(sg PUBLIC ${PLIB_SOURCE_DIR}/src/sg)

ADD_LIBRARY(fnt STATIC ${FNT_SRCS} ${FNT_PUBLIC_HEADERS} ${FNT_PRIVATE_HEADERS})

TARGET_INCLUDE_DIRECTORIES(fnt PUBLIC ${PLIB_SOURCE_DIR}/src/fnt)
TARGET_INCLUDE_DIRECTORIES(fnt PUBLIC ${PLIB_SOURCE_DIR}/src/sg)

ADD_LIBRARY(js STATIC ${JS_SRCS} ${JS_PUBLIC_HEADERS} ${JS_PRIVATE_HEADERS})

ADD_LIBRARY(ul STATIC ${UL_SRCS} ${UL_PUBLIC_HEADERS} ${UL_PRIVATE_HEADERS})

ADD_LIBRARY(pui STATIC ${PUI_SRCS} ${PUI_PUBLIC_HEADERS} ${PUI_PRIVATE_HEADERS})
TARGET_INCLUDE_DIRECTORIES(pui PUBLIC ${PLIB_SOURCE_DIR}/src/pui)
TARGET_LINK_LIBRARIES(pui PUBLIC fnt)

ADD_LIBRARY(puAux STATIC ${PUAUX_SRCS} ${PUAUX_PUBLIC_HEADERS} ${PUAUX_PRIVATE_HEADERS})
TARGET_INCLUDE_DIRECTORIES(pui PUBLIC ${PLIB_SOURCE_DIR}/src/puAux)

TARGET_LINK_LIBRARIES(puAux PUBLIC fnt pui)

set(PLIB_TARGETS sg fnt js ul pui puAux)

# Runtime equals DLL-files
# Archive equals static libraries
# Library equals module libraries
IF(NOT SKIP_INSTALL_LIBRARIES AND NOT SKIP_INSTALL_ALL )
	install(TARGETS ${PLIB_TARGETS}
		RUNTIME DESTINATION ${EXECUTABLE_OUTPUT_PATH}
		LIBRARY DESTINATION ${LIBRARY_OUTPUT_PATH}
		ARCHIVE DESTINATION ${ARCHIVE_OUTPUT_PATH})
ENDIF()
IF(NOT SKIP_INSTALL_HEADERS AND NOT SKIP_INSTALL_ALL )
	install(FILES ${JS_PUBLIC_HEADERS}
					${UL_PUBLIC_HEADERS}
					${SG_PUBLIC_HEADERS}
				${FNT_PUBLIC_HEADERS}
				${PUI_PUBLIC_HEADERS}
				${PUAUX_PUBLIC_HEADERS}
			DESTINATION ${INCLUDE_OUTPUT_PATH}/plib)
ENDIF()
