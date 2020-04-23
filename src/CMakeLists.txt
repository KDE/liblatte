set(LATTE_LIB_NAME "Latte")
set(LATTE_LIB_VERSION 3)
set(LATTE_LIB_SOVERSION "1")

set(Latte_LIB_SRCS
    latte.cpp    
)

add_library(${LATTE_LIB_NAME} SHARED ${Latte_LIB_SRCS})

ecm_generate_export_header(Latte
    EXPORT_FILE_NAME latte/latte_export.h
    BASE_NAME Latte
    VERSION ${LATTE_LIB_VERSION}
)

target_link_libraries(${LATTE_LIB_NAME}
    Qt5::Quick
)

set(Latte_BUILD_INCLUDE_DIRS
    ${CMAKE_CURRENT_SOURCE_DIR}/..
    ${CMAKE_CURRENT_BINARY_DIR}
    ${CMAKE_CURRENT_BINARY_DIR}/Latte
)

set(Latte_HEADERS
    ${CMAKE_CURRENT_SOURCE_DIR}/latte.h
)

target_include_directories(${LATTE_LIB_NAME} PUBLIC
  "$<BUILD_INTERFACE:${Latte_BUILD_INCLUDE_DIRS}>"
)

target_include_directories(${LATTE_LIB_NAME} INTERFACE
  "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR};${CMAKE_INSTALL_INCLUDEDIR}/Latte>"
)

set_target_properties(${LATTE_LIB_NAME} PROPERTIES
                                        VERSION ${LATTE_LIB_VERSION}
                                        SOVERSION ${LATTE_LIB_SOVERSION}
                                        EXPORT_NAME ${LATTE_LIB_NAME}
                      )

################ install files ###############
ecm_generate_headers(Latte_CamelCase_HEADERS
    HEADER_NAMES
        Latte
    REQUIRED_HEADERS Latte_HEADERS
    PREFIX Latte
)


install(TARGETS ${LATTE_LIB_NAME} EXPORT LatteConfig
    ARCHIVE  DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY  DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME  DESTINATION ${CMAKE_INSTALL_BINDIR})

install(FILES
        ${Latte_HEADERS}
        ${CMAKE_CURRENT_BINARY_DIR}/latte/latte_export.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/latte)

install(FILES
        ${Latte_CamelCase_HEADERS}
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/Latte)
        
install(EXPORT LatteConfig DESTINATION share/Latte/cmake)

export(TARGETS Latte FILE Latte.cmake)
