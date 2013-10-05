cmake_minimum_required(VERSION 2.8)


include_directories(srcglfw3/include)

FIND_LIBRARY(GLFW3LIBRARY glfw3 /srcglfw3/src/libglfw3.a)


add_executable(test maintest.c)
TARGET_LINK_LIBRARIES(test ${GLFW3LIBRARY})
add_dependencies(test glfw3)

if(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    target_link_libraries(test glfw3 ${X11_LIBRARY})
endif(${CMAKE_SYSTEM_NAME} MATCHES "Linux")

if(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    FIND_LIBRARY(COCOA_LIBRARY Cocoa)
    FIND_LIBRARY(APPLICATION_SERVICES_LIBRARY ApplicationServices)
    FIND_LIBRARY(OGL_LIBRARY OpenGL)
    FIND_LIBRARY(AGL_LIBRARY AGL)
    FIND_LIBRARY(IOKIT IOKit)
    target_link_libraries(test glfw3 ${IOKIT} ${COCOA_LIBRARY} ${APPLICATION_SERVICES_LIBRARY} ${OGL_LIBRARY} ${AGL_LIBRARY})
endif(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
