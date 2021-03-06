cmake_minimum_required(VERSION 3.5)

project(caplibpp_unit_test LANGUAGES CXX)

add_definitions(-DGTEST_LANGUAGE_CXX11)

find_package(Threads REQUIRED)

if ($ENV{GOOGLETEST_DIR})
    set(GOOGLETEST_DIR $ENV{GOOGLETEST_DIR})
else ()
    if (NOT "" STREQUAL "")
        message(WARNING "Using googletest src dir specified at Qt Creator wizard")
    endif ()
    set(GOOGLETEST_DIR "")
endif ()
if (EXISTS ${GOOGLETEST_DIR})
    set(GTestSrc ${GOOGLETEST_DIR}/googletest)
    set(GMockSrc ${GOOGLETEST_DIR}/googlemock)
elseif (UNIX AND EXISTS /usr/src/gtest)
    set(GTestSrc /usr/src/gtest)
    message(WARNING "Using gtest from system")
    if (EXISTS /usr/src/gmock)
        set(GMockSrc /usr/src/gmock)
    endif ()
else ()
    message( FATAL_ERROR "No googletest src dir found - set GOOGLETEST_DIR to enable!")
endif ()

set(GTestFiles ${GTestSrc}/src/gtest-all.cc)
set(GTestIncludes ${GTestSrc} ${GTestSrc}/include)
if (NOT ${GMockSrc} STREQUAL "")
    list(APPEND GTestFiles ${GMockSrc}/src/gmock-all.cc)
    list(APPEND GTestIncludes ${GMockSrc} ${GMockSrc}/include)
endif ()

include_directories(${GTestIncludes})
file(GLOB_RECURSE TESTINC_FILES *.h)
target_include_directories(CAPLibpp PUBLIC ${PROJECT_SOURCE_DIR}/include)

add_executable(caplibpp_unit_test main.cpp ${TESTINC_FILES}
               ${GTestFiles})
add_test(NAME caplibpp_unit_test COMMAND caplibpp_unit_test)
target_link_libraries(caplibpp_unit_test PRIVATE Threads::Threads)
target_link_libraries(caplibpp_unit_test PRIVATE CAPLibpp)
target_link_libraries(caplibpp_unit_test PUBLIC ${CURL_LIBRARIES})
target_link_libraries(caplibpp_unit_test PUBLIC ${BOOST_LIBRARIES})
target_link_libraries(caplibpp_unit_test PUBLIC ${CURLPP_LIBRARIES})
target_link_libraries(caplibpp_unit_test PUBLIC ${OPENSSL_LIBRARIES})

