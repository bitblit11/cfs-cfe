# Generate documentation
find_package(Doxygen)
if(DOXYGEN_FOUND)
    configure_file(${CMAKE_CURRENT_SOURCE_DIR}/detail_doxy.in ${CMAKE_CURRENT_BINARY_DIR}/detail_doxy @ONLY)
    configure_file(${CMAKE_CURRENT_SOURCE_DIR}/user_doxy.in ${CMAKE_CURRENT_BINARY_DIR}/user_doxy @ONLY)
    add_custom_target(cfe-docs
    	COMMAND mkdir -p ${CMAKE_BINARY_DIR}/docs/users_guide/html/cfe/
    	COMMAND mkdir -p ${CMAKE_BINARY_DIR}/docs/users_guide/latex/cfe/
    	COMMAND mkdir -p ${CMAKE_BINARY_DIR}/docs/detailed_design/html/cfe/
    	COMMAND mkdir -p ${CMAKE_BINARY_DIR}/docs/detailed_design/latex/cfe/
        COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/user_doxy
        COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/detail_doxy
        WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/
        COMMENT "Generating API documentation with Doxygen" VERBATIM
    )
endif(DOXYGEN_FOUND)