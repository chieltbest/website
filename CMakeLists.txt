cmake_minimum_required(VERSION 3.6)
project(website)

add_custom_command(
		OUTPUT ${CMAKE_CURRENT_LIST_DIR}/local/index.html
		COMMAND cp ../index.tex ../index.cfg .
		COMMAND make4ht -l -s -d ../local -c index.cfg index.tex
#		COMMAND biber build/main.bcf
		WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
		DEPENDS index.tex index.cfg
)

set_source_files_properties(${CMAKE_CURRENT_LIST_DIR}/build/ GENERATED)

add_custom_target(website DEPENDS ${CMAKE_CURRENT_LIST_DIR}/local/index.html)
