FILE(GLOB OSSIM_APP_DIRS "ossim-*")
FILE(GLOB OSSIM_CONFIG_DIR "ossim-config*")
LIST(REMOVE_ITEM OSSIM_APP_DIRS ${OSSIM_CONFIG_DIR})

FIND_PACKAGE(ossim)
FIND_PACKAGE( OpenThreads )
if( OPENTHREADS_FOUND )
   include_directories( ${OPENTHREADS_INCLUDE_DIR} )
else( OPENTHREADS_FOUND )
   message( FATAL_ERROR "Could not find required OpenThreads package!" )
endif( OPENTHREADS_FOUND )

if( OSSIM_FOUND )
   include_directories( ${OSSIM_INCLUDE_DIR} )
else( OSSIM_FOUND )
   message( FATAL_ERROR "Could not find required OSSIM package!" )
endif( OSSIM_FOUND )
set(TARGET_COMMON_LIBRARIES ${OSSIM_LIBRARY} ${OPENTHREADS_LIBRARY})

FOREACH(f ${OSSIM_APP_DIRS})
	ADD_SUBDIRECTORY(${f})
ENDFOREACH(f)

ADD_SUBDIRECTORY(ossimtool)
