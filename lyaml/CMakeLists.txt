cmake_minimum_required(VERSION 3.10)

project(luapower-lyaml C)

if(NOT DEFINED LUA_INCLUDE_DIR OR NOT DEFINED LUA_LIBRARIES)
    find_package(Lua REQUIRED)
endif()

add_definitions(
	-DPACKAGE="lyaml"
	-DVERSION="yasuo"
)

include_directories(
	${LUA_INCLUDE_DIR}
	${PROJECT_SOURCE_DIR}/tmpinc
)

link_directories(
	${LUA_LIBRARIES}
	${PROJECT_SOURCE_DIR}/tmplib
)

add_library(yaml MODULE
	lyaml/ext/yaml/emitter.c
	lyaml/ext/yaml/parser.c
	lyaml/ext/yaml/scanner.c
	lyaml/ext/yaml/yaml.c
)

target_link_libraries(yaml -lyaml)

set_target_properties(yaml PROPERTIES PREFIX "")

