cmake_minimum_required(VERSION 3.20 FATAL_ERROR)

project(TMPL VERSION 1.0 LANGUAGES C CXX)

set(TMPL_HOME ${CMAKE_CURRENT_LIST_DIR})

set(TMPL_INCLUDE_DIR ${TMPL_HOME}/include)
set(TMPL_SOURCES_DIR ${TMPL_HOME}/sources)

# FOO Library

file(GLOB_RECURSE FOO_PUBLIC_HEADERS CONFIGURE_DEPENDS
	${TMPL_INCLUDE_DIR}/foo/*.hpp
	${TMPL_INCLUDE_DIR}/foo/*.inl
	${TMPL_INCLUDE_DIR}/foo/*.h
)

file(GLOB_RECURSE FOO_SOURCES CONFIGURE_DEPENDS
	${TMPL_SOURCES_DIR}/foo/*.cpp
	${TMPL_SOURCES_DIR}/foo/*.c
	${TMPL_SOURCES_DIR}/foo/*.hpp
	${TMPL_SOURCES_DIR}/foo/*.inl
	${TMPL_SOURCES_DIR}/foo/*.h
)

add_library(foo STATIC ${FOO_SOURCES} ${FOO_PUBLIC_HEADERS})

target_include_directories(foo PUBLIC ${TMPL_INCLUDE_DIR})

# TMPL Executable

file(GLOB_RECURSE TMPL_SOURCES CONFIGURE_DEPENDS
	${TMPL_SOURCES_DIR}/tmpl/*.cpp
	${TMPL_SOURCES_DIR}/tmpl/*.c
	${TMPL_SOURCES_DIR}/tmpl/*.hpp
	${TMPL_SOURCES_DIR}/tmpl/*.inl
	${TMPL_SOURCES_DIR}/tmpl/*.h
)

add_executable(tmpl ${TMPL_SOURCES})

target_include_directories(tmpl PUBLIC ${TMPL_INCLUDE_DIR})

target_link_libraries(tmpl PUBLIC foo)
