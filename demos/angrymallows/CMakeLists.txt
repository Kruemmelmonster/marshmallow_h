file(GLOB ANGRYMALLOWS_DEMO_SRCS *.cpp)

add_executable(angrymallows_demo ${ANGRYMALLOWS_DEMO_SRCS})

# BOX2D
include_directories(${BOX2D_INCLUDE_DIR})

if (MARSHMALLOW_DEMO_CWD_OVERRIDE)
	if (APPLE)
		# Xcode workaround
		set_target_properties(angrymallows_demo PROPERTIES
		    COMPILE_FLAGS -DDEMO_CWD=\\\\"${CMAKE_CURRENT_SOURCE_DIR}\\\\")
	else ()
		set_target_properties(angrymallows_demo PROPERTIES
		    COMPILE_FLAGS -DDEMO_CWD=\\"${CMAKE_CURRENT_SOURCE_DIR}\\")
	endif()
endif()

if(WIN32 AND NOT MARSHMALLOW_DEBUG)
	set_target_properties(angrymallows_demo PROPERTIES WIN32_EXECUTABLE ON)
endif()

target_link_libraries(angrymallows_demo marshmallow_entrypoint
                                        marshmallow_game
                                        ${BOX2D_LIBRARIES})

install(TARGETS angrymallows_demo
        RUNTIME DESTINATION bin COMPONENT demos)

install(DIRECTORY assets/
        DESTINATION assets COMPONENT demos)

