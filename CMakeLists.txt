cmake_minimum_required(VERSION 3.14)

project(
    libaffa 
    VERSION 0.9.6
    DESCRIPTION "An affine arithmetic C++ library"
    LANGUAGES CXX
    )

SET(AFFA_HEADER aa_aaf.h aa.h aa_interval.h aa_rounding.h aa_util.h)
SET(AFFA_SOURCE aa_aafapprox.cpp aa_aafarithm.cpp aa_aafcommon.cpp aa_aaftrigo.cpp aa_interval.cpp aa_rounding.cpp)

add_library(
    affa 
    SHARED 
    ${AFFA_SOURCE}
)
set(MYFLAGS -Wall -Wno-deprecated -O3)
target_compile_options(affa PRIVATE ${MYFLAGS})
set_target_properties(
    affa PROPERTIES
    SOVERSION 0
    VERSION 0.9.6
    )

add_library(
    affa.static
    STATIC 
    ${AFFA_SOURCE}
)
set_target_properties(
    affa.static PROPERTIES
    SOVERSION 0
    VERSION 0.9.6
    )

target_compile_options(affa.static PRIVATE ${MYFLAGS})
set_target_properties(affa.static PROPERTIES OUTPUT_NAME affa)

include(GNUInstallDirs)
set(AFFA_INSTALL_INCLUDEDIR ${CMAKE_INSTALL_INCLUDEDIR}/affa)
install(FILES ${AFFA_HEADER} DESTINATION ${AFFA_INSTALL_INCLUDEDIR} COMPONENT devel)
install(TARGETS affa DESTINATION ${CMAKE_INSTALL_LIBDIR} COMPONENT core)
install(TARGETS affa.static DESTINATION ${CMAKE_INSTALL_LIBDIR} COMPONENT core)

