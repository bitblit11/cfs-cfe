# Set what we're going to call the executable file.
set(CFE_EXEC_FILE core-bin)

# Where to put applications
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${INSTALL_DIR} PARENT_SCOPE)

# Where to put tables
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${INSTALL_DIR} PARENT_SCOPE)

# Collect CFE includes and sources
set(CFE_INC_DIRS 
	${CMAKE_CURRENT_SOURCE_DIR}/../es
	${CMAKE_CURRENT_SOURCE_DIR}/../evs
	${CMAKE_CURRENT_SOURCE_DIR}/../fs
	${CMAKE_CURRENT_SOURCE_DIR}/../inc
	${CMAKE_CURRENT_SOURCE_DIR}/../sb
	${CMAKE_CURRENT_SOURCE_DIR}/../tbl
	${CMAKE_CURRENT_SOURCE_DIR}/../time)
	
add_subdirectory(../es es)
add_subdirectory(../evs evs)
add_subdirectory(../fs fs)
add_subdirectory(../sb sb)
add_subdirectory(../tbl tbl)
add_subdirectory(../time time)

set(CFE_SRC ${CFE_ES_SRC} ${CFE_EVS_SRC} ${CFE_FS_SRC} ${CFE_SB_SRC} ${CFE_TBL_SRC} ${CFE_TIME_SRC})

# Add CMake files from OSAL and PSP
add_subdirectory($ENV{OSAL_SRC}/${OS} osal)
add_subdirectory($ENV{CFE_PSP_SRC}/${PSP}/make psp)

# Add global include directories.
include_directories(${CFE_INC_DIRS})
include_directories(${OSAL_INC_DIRS})
include_directories(${PSP_INC_DIRS})

# Add the executable
add_executable(${CFE_EXEC_FILE} ${CFE_SRC} ${OSAL_SRC} ${PSP_SRC})
set_target_properties(${CFE_EXEC_FILE} PROPERTIES ENABLE_EXPORTS TRUE)
target_link_libraries(${CFE_EXEC_FILE} ${LIBS})
set_target_properties(${CFE_EXEC_FILE} PROPERTIES COMPILE_FLAGS ${COMPILE_FLAGS} LINK_FLAGS ${LINK_FLAGS})
set_target_properties(${CFE_EXEC_FILE} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${INSTALL_DIR})

# Generate documentation
add_subdirectory($ENV{CFE_DIR}/docs docs)

# Build and run unit tests
add_subdirectory($ENV{CFE_CORE_SRC}/../unit-test cfe-ut)

# Collect UTF source code and header files required by the application unit tests.
add_subdirectory($ENV{CFE_DIR}/tools/utf utf)

# Pass some variables up to the parent.
set(COMPILE_FLAGS ${COMPILE_FLAGS} PARENT_SCOPE)
set(LINK_FLAGS ${LINK_FLAGS} PARENT_SCOPE)
set(CFE_INC_DIRS ${CFE_INC_DIRS} PARENT_SCOPE)
set(OSAL_INC_DIRS ${OSAL_INC_DIRS} PARENT_SCOPE)
set(PSP_INC_DIRS ${PSP_INC_DIRS} PARENT_SCOPE)
set(CMAKE_C_COMPILER ${CMAKE_C_COMPILER} PARENT_SCOPE)
set(CMAKE_C_FLAGS ${CMAKE_C_FLAGS} PARENT_SCOPE)
set(CMAKE_CXX_COMPILER ${CMAKE_CXX_COMPILER} PARENT_SCOPE)
set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} PARENT_SCOPE)
SET(UTF_SRC ${UTF_SRC} PARENT_SCOPE)
SET(UTF_INCS ${UTF_INCS} PARENT_SCOPE)