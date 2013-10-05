cmake_minimum_required(VERSION 2.8)


include_directories(srcglfw3/include)
add_subdirectory(srcglfw3)
set (EXTRA_LIBS ${EXTRA_LIBS} srcglfw3)


add_executable(test maintest.c)

if(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    target_link_libraries(test ${EXTRA_LIBS} ${X11_LIBRARY})
endif(${CMAKE_SYSTEM_NAME} MATCHES "Linux")

if(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    FIND_LIBRARY(COCOA_LIBRARY Cocoa)
    FIND_LIBRARY(APPLICATION_SERVICES_LIBRARY ApplicationServices)
    FIND_LIBRARY(OGL_LIBRARY OpenGL)
    FIND_LIBRARY(AGL_LIBRARY AGL)
    FIND_LIBRARY(IOKIT IOKit)
    target_link_libraries(test ${EXTRA_LIBS} ${IOKIT} ${COCOA_LIBRARY} ${APPLICATION_SERVICES_LIBRARY} ${OGL_LIBRARY} ${AGL_LIBRARY})
endif(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
