project(xrLuaFix)

set(SRC_FILES
    "LibMath.cpp"
    "LibMath.h"
    "LibStr.cpp"
    "LibStr.h"
    "LibTab.cpp"
    "LibTab.h"
    "Logger.cpp"
    "Logger.h"
    "xrLuaFix.cpp"
    "xrLuaFix.h"
)

set(PCH_FILES
    "pch.cpp"
    "pch.hpp"
)

set(LFS_FILES
    "lfs/src/lfs.c"
    "lfs/src/lfs.h"
)

set(LMARSHAL_FILES
    "lua-marshal/lmarshal.c"
)
set(LPACK_FILES
    "lua-pack/lua_pack.c"
)

source_group("pch" FILES ${PCH_FILES})

source_group("lfs" FILES ${LFS_FILES})
source_group("lmarshal" FILES ${LMARSHAL_FILES})
source_group("lpack" FILES ${LPACK_FILES})

add_library(${PROJECT_NAME} STATIC
    ${SRC_FILES}
    ${PCH_FILES}
    ${LFS_FILES}
    ${LMARSHAL_FILES}
    ${LPACK_FILES}
)

target_include_directories(${PROJECT_NAME}
    PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/lfs/src
    ${LUA_INCLUDE_DIR}
    ${CMAKE_SOURCE_DIR}/src
)

target_link_libraries(${PROJECT_NAME}
    PRIVATE
    xrCore
    ${LUA_LIBRARIES}
)

# XXX: doesn't compile
#target_precompile_headers(${PROJECT_NAME}
#    PRIVATE
#    "pch.hpp"
#)

set_target_properties(${PROJECT_NAME} PROPERTIES
    PREFIX ""
    POSITION_INDEPENDENT_CODE ON
)
