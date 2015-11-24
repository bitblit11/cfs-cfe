include(CTest)
find_program( MEMORYCHECK_COMMAND valgrind )
set( MEMORYCHECK_COMMAND_OPTIONS "--trace-children=yes --leak-check=full" )

# Set include directories
include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}
	${CFE_INC_DIRS})

#set(CFE_SRCA ${CFE_ES_SRC} ${CFE_EVS_SRC} ${CFE_FS_SRC} ${CFE_SB_SRC} ${CFE_TBL_SRC} ${CFE_TIME_SRC})

add_definitions(-DCFE_LINUX)

set(CMAKE_CXX_FLAGS "-g -O0 -Wall -W -Wshadow -Wunused-variable 
	-Wunused-parameter -Wunused-function -Wunused -Wno-system-headers 
	-Wno-deprecated -Woverloaded-virtual -Wwrite-strings -fprofile-arcs 
	-ftest-coverage -m32")
set(CMAKE_C_FLAGS "-g -O0 -Wall -W -fprofile-arcs -ftest-coverage -m32")

# Add the executables
add_executable(es_UT 
		${CMAKE_CURRENT_SOURCE_DIR}/es_UT.c 
		${CMAKE_CURRENT_SOURCE_DIR}/ut_stubs.c 
		${CMAKE_CURRENT_SOURCE_DIR}/ut_bsp_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_osapi_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_evs_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_sb_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_fs_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_tbl_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_time_stubs.c
		${CFE_ES_SRC})
target_link_libraries(es_UT -fprofile-arcs gcov)
add_test(cfe-es ${EXECUTABLE_OUTPUT_PATH}/es_UT)

add_executable(evs_UT 
		${CMAKE_CURRENT_SOURCE_DIR}/evs_UT.c 
		${CMAKE_CURRENT_SOURCE_DIR}/ut_stubs.c 
		${CMAKE_CURRENT_SOURCE_DIR}/ut_bsp_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_osapi_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_es_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_sb_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_fs_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_tbl_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_time_stubs.c
		${CFE_EVS_SRC})
target_link_libraries(evs_UT -fprofile-arcs gcov)
add_test(cfe-evs ${EXECUTABLE_OUTPUT_PATH}/evs_UT)

add_executable(sb_UT 
		${CMAKE_CURRENT_SOURCE_DIR}/sb_UT.c 
		${CMAKE_CURRENT_SOURCE_DIR}/ut_stubs.c 
		${CMAKE_CURRENT_SOURCE_DIR}/ut_bsp_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_osapi_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_es_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_evs_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_fs_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_tbl_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_time_stubs.c
		${CFE_SB_SRC})
target_link_libraries(sb_UT -fprofile-arcs gcov)
add_test(cfe-sb ${EXECUTABLE_OUTPUT_PATH}/sb_UT)

add_executable(fs_UT 
		${CMAKE_CURRENT_SOURCE_DIR}/fs_UT.c 
		${CMAKE_CURRENT_SOURCE_DIR}/ut_stubs.c 
		${CMAKE_CURRENT_SOURCE_DIR}/ut_bsp_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_osapi_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_es_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_evs_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_sb_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_tbl_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_time_stubs.c
		${CFE_FS_SRC})
target_link_libraries(fs_UT -fprofile-arcs gcov)
add_test(cfe-fs ${EXECUTABLE_OUTPUT_PATH}/fs_UT)

add_executable(tbl_UT 
		${CMAKE_CURRENT_SOURCE_DIR}/tbl_UT.c 
		${CMAKE_CURRENT_SOURCE_DIR}/ut_stubs.c 
		${CMAKE_CURRENT_SOURCE_DIR}/ut_bsp_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_osapi_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_es_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_evs_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_sb_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_fs_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_time_stubs.c
		${CFE_TBL_SRC})
target_link_libraries(tbl_UT -fprofile-arcs gcov)
add_test(cfe-tbl ${EXECUTABLE_OUTPUT_PATH}/tbl_UT)

add_executable(time_UT 
		${CMAKE_CURRENT_SOURCE_DIR}/time_UT.c 
		${CMAKE_CURRENT_SOURCE_DIR}/ut_stubs.c 
		${CMAKE_CURRENT_SOURCE_DIR}/ut_bsp_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_osapi_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_es_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_evs_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_sb_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_fs_stubs.c
		${CMAKE_CURRENT_SOURCE_DIR}/ut_tbl_stubs.c
		${CFE_TIME_SRC})
target_link_libraries(time_UT -fprofile-arcs gcov)
add_test(cfe-time ${EXECUTABLE_OUTPUT_PATH}/time_UT)

add_definitions(-fprofile-arcs -ftest-coverage)
