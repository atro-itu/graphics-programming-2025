# ---------------------------------------------------------------------------------
# Projects Settings
# ---------------------------------------------------------------------------------
cmake_minimum_required(VERSION 3.3)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

MACRO(SUBDIRLIST result curdir)
    FILE(GLOB children RELATIVE ${curdir} ${curdir}/*)
    SET(dirlist "")
    FOREACH(child ${children})
        IF(IS_DIRECTORY ${curdir}/${child})
            LIST(APPEND dirlist ${child})
        ENDIF()
    ENDFOREACH()
    SET(${result} ${dirlist})
ENDMACRO()


if(APPLE)
    set(APPLE_LIBRARIES
      "-framework OpenGL"
      "-framework Cocoa"
      "-framework IOKit"
      "-framework CoreVideo"
	)
endif()

# ---------------------------------------------------------------------------------
# Cmake projects
# ---------------------------------------------------------------------------------
project(ITU-graphics-programming)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

set(FBX_SUPPORT OFF)

set(LIBRARIES_SOURCE_PATH ${CMAKE_SOURCE_DIR}/libraries)
include_directories(
	${LIBRARIES_SOURCE_PATH}/glad/include
	${LIBRARIES_SOURCE_PATH}/glfw/include
	${LIBRARIES_SOURCE_PATH}/imgui/include
	${LIBRARIES_SOURCE_PATH}/glm/include
	${LIBRARIES_SOURCE_PATH}/stb/include
	${LIBRARIES_SOURCE_PATH}/assimp/include
	${LIBRARIES_SOURCE_PATH}/assimp
	${LIBRARIES_SOURCE_PATH}/itugl/include
)

add_subdirectory(${CMAKE_SOURCE_DIR}/libraries)
add_subdirectory(${CMAKE_SOURCE_DIR}/exercises)
