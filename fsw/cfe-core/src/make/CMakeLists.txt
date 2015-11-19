SET(CFE_INC_DIRS 
	${CMAKE_CURRENT_SOURCE_DIR}/../es
	${CMAKE_CURRENT_SOURCE_DIR}/../evs
	${CMAKE_CURRENT_SOURCE_DIR}/../fs
	${CMAKE_CURRENT_SOURCE_DIR}/../inc
	${CMAKE_CURRENT_SOURCE_DIR}/../sb
	${CMAKE_CURRENT_SOURCE_DIR}/../tbl
	${CMAKE_CURRENT_SOURCE_DIR}/../time 
	PARENT_SCOPE)

add_subdirectory(../es es)
add_subdirectory(../evs evs)
add_subdirectory(../fs fs)
add_subdirectory(../sb sb)
add_subdirectory(../tbl tbl)
add_subdirectory(../time time)

SET(CFE_SRC ${CFE_ES_SRC} ${CFE_EVS_SRC} ${CFE_FS_SRC} ${CFE_SB_SRC} ${CFE_TBL_SRC} ${CFE_TIME_SRC} PARENT_SCOPE)
