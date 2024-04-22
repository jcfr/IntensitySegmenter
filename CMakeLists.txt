cmake_minimum_required(VERSION 2.8.10)

project(IntensitySegmenter)

if( IntensitySegmenter_BUILD_SLICER_EXTENSION )
  #-----------------------------------------------------------------------------
  # Extension meta-information
  set(EXTENSION_HOMEPAGE "https://www.nitrc.org/projects/dentaltools/")
  set(EXTENSION_CATEGORY "Segmentation")
  set(EXTENSION_CONTRIBUTORS "Pengdong Xiao (Department of Orthodontics, UNC), Beatriz Paniagua (Department of Orthodontics, UNC), Francois Budin (NIRAL, UNC)")
  set(EXTENSION_DESCRIPTION "IntensitySegmenter is a simple tool that segments an image according to intensity value. It is mainly used to segment CT scans using the Hounsfield scale but the ranges of intensities and their corresponding labels can be specified in an input text file.")
  set(EXTENSION_ICONURL "https://wiki.slicer.org/slicerWiki/images/f/f6/IntensitySegmenterIcon.png")
  set(EXTENSION_SCREENSHOTURLS "https://wiki.slicer.org/slicerWiki/images/7/7c/IntensitySegmenter-OutputScreenshot.png")
  #-----------------------------------------------------------------------------
  # Extension dependencies
  find_package( Slicer REQUIRED )
  include( ${Slicer_USE_FILE} )
else()
  set( STATIC "EXECUTABLE_ONLY" )
  find_package( SlicerExecutionModel REQUIRED )
  include( ${SlicerExecutionModel_USE_FILE} )
  find_package( ITK REQUIRED )
  include( ${ITK_USE_FILE} )
endif()

set( MyModule_NAME IntensitySegmenter )

set(MyModule_SOURCE
    ${MyModule_NAME}.cxx )

SEMMacroBuildCLI(
  NAME ${MyModule_NAME}
  ${STATIC}
  TARGET_LIBRARIES ${ITK_LIBRARIES}
  )

option(BUILD_TESTING "Build the testing tree" ON)
if(BUILD_TESTING)
  add_subdirectory(Testing)
endif()

if( IntensitySegmenter_BUILD_SLICER_EXTENSION )
  include(${Slicer_EXTENSION_CPACK})
endif()
