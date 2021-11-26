cmake_minimum_required(VERSION 3.1.0)

project(QtPDF)

set(CMAKE_CXX_STANDARD 14)

IF (WIN32)
	MESSAGE(STATUS "Now is windows")
	set(CMAKE_PREFIX_PATH "C:\\Qt\\5.15.2\\msvc2019_64\\bin")
	set(Qt5_DIR "C:\\Qt\\5.15.2\\msvc2019_64\\lib\\cmake\\Qt5")
	set(PDFium_DIR "${CMAKE_SOURCE_DIR}/3rdparty/pdfium-win-x64")
ELSEIF (APPLE)
	MESSAGE(STATUS "Now is Apple systens.")
ELSEIF (UNIX)
	MESSAGE(STATUS "Now is UNIX-like OS's.")
ENDIF ()

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

if(CMAKE_VERSION VERSION_LESS "3.7.0")
    set(CMAKE_INCLUDE_CURRENT_DIR ON)
endif()


add_definitions(-DQT_BUILD_PDF_LIB) #定义导出宏


include_directories(./
					./pdf/api/
					./QtPdf/				
)

find_package(Qt5 COMPONENTS Widgets REQUIRED)
get_target_property(QtCore_location Qt5::Widgets LOCATION)


find_package(Qt5 COMPONENTS Core REQUIRED)
get_target_property(QtCore_location Qt5::Core LOCATION)

find_package(Qt5 COMPONENTS Network REQUIRED)
get_target_property(QtCore_location Qt5::Network LOCATION)

add_library(QtPDF SHARED 
	# ./pdf/qtpdf-config.h
	#./pdf/api/qtpdfglobal.h
	# ./pdf/qpdfselection.cpp
	# ./pdf/api/qpdfselection.h
	# ./pdf/api/qpdfselection_p.h
	./pdf/api/qpdfbookmarkmodel.h
	./pdf/api/qpdfdestination_p.h
	./pdf/api/qpdfdestination.h
	./pdf/api/qpdfdocument_p.h
	./pdf/api/qpdfdocument.h
	./pdf/api/qpdfdocumentrenderoptions.h
	./pdf/api/qpdflinkmodel_p_p.h
	./pdf/api/qpdflinkmodel_p.h
	./pdf/api/qpdfnamespace.h
	./pdf/api/qpdfpagenavigation.h
	./pdf/api/qpdfpagerenderer.h
	./pdf/api/qpdfsearchmodel_p.h
	./pdf/api/qpdfsearchmodel.h
	./pdf/api/qpdfsearchresult_p.h
	./pdf/api/qpdfsearchresult.h
	./pdf/api/qpdfselection_p.h
	./pdf/api/qpdfselection.h


	./pdf/qpdfdestination.cpp
	./pdf/qpdfdocument.cpp
	./pdf/qpdfbookmarkmodel.cpp
	./pdf/qpdflinkmodel.cpp
	./pdf/qpdfpagenavigation.cpp
	./pdf/qpdfpagerenderer.cpp
	./pdf/qpdfsearchmodel.cpp
	./pdf/qpdfsearchresult.cpp
	./pdf/qpdfselection.cpp
)

find_package(PDFium)

target_link_libraries(QtPDF Qt5::Widgets Qt5::Core Qt5::GuiPrivate Qt5::CorePrivate Qt5::Network pdfium)

#todo windows copy
add_custom_command(TARGET ${PROJECT_NAME}
  PRE_BUILD 
  COMMAND echo "executing a fake command"
  COMMENT "This command will be executed before building target Test1"
 )
