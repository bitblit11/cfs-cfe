# Collect source and includes
set(ELF2CFETBL_SRC 
	${CMAKE_CURRENT_SOURCE_DIR}/elf2cfetbl.c 
	PARENT_SCOPE)
	
set(ELF2CFETBL_INC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../../fsw/cfe-core/src/inc
    ${CMAKE_CURRENT_SOURCE_DIR}/../../fsw/cfe-core/src/tbl
    ${CMAKE_CURRENT_SOURCE_DIR}/../../../OSAL/src/os/inc
    ${CMAKE_CURRENT_SOURCE_DIR}/../../../PSP/fsw/inc
    ${CMAKE_CURRENT_SOURCE_DIR}/../../../PSP/fsw/pc-linux/inc
    PARENT_SCOPE)

set(COMPILE_FLAGS "${COMPILE_FLAGS} -Wformat=0" PARENT_SCOPE)
