###############################################################################
# Package: DetCRD
#   CEPC Reference Detector (CRD)
################################################################################
gaudi_subdir(DetCRD v0r0)

gaudi_depends_on_subdirs(GaudiKernel)


find_package(DD4hep COMPONENTS DDRec DDG4 DDParsers REQUIRED)
# find_package(DD4hep)
find_package(Geant4)
include(${Geant4_USE_FILE})

set(CMAKE_MODULE_PATH  ${CMAKE_MODULE_PATH}  ${DD4hep_ROOT}/cmake )
include( DD4hep )

find_package(ROOT COMPONENTS MathCore GenVector Geom REQUIRED)

install(DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/compact DESTINATION Detector/DetCRD)

set(DetCRD_src
    src/Calorimeter/CRDEcal.cpp
    src/Other/CRDBeamPipe_v01_geo.cpp
)

gaudi_add_module(DetCRD
                  ${DetCRD_src}
		  INCLUDE_DIRS 
                  # DD4hep 
                  # ROOT 
                  # Geant4 
                  src/include
		  LINK_LIBRARIES
                  # GaudiKernel
                  DD4hep
                  ${DD4hep_COMPONENT_LIBRARIES}
                  # ROOT 
                  # Geant4
)

set(LIBRARY_OUTPUT_PATH ${CMAKE_LIBRARY_OUTPUT_DIRECTORY})
message(STATUS "LIBRARY_OUTPUT_PATH -> ${LIBRARY_OUTPUT_PATH}")
dd4hep_generate_rootmap(DetCRD)
