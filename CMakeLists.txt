set(BOOST_SOURCE ${CMAKE_CURRENT_SOURCE_DIR})

file(STRINGS "${BOOST_SOURCE}/boost/version.hpp" boost_version_raw
  REGEX "define BOOST_VERSION "
)
string(REGEX MATCH "[0-9]+" boost_version_raw "${boost_version_raw}")
math(EXPR BOOST_VERSION_MAJOR "${boost_version_raw} / 100000")
math(EXPR BOOST_VERSION_MINOR "${boost_version_raw} / 100 % 1000")
math(EXPR BOOST_VERSION_PATCH "${boost_version_raw} % 100")
set(BOOST_VERSION "${BOOST_VERSION_MAJOR}.${BOOST_VERSION_MINOR}.${BOOST_VERSION_PATCH}")

message(STATUS "Boost-trim found: ${BOOST_VERSION} ${BOOST_SOURCE}")

add_library(Boost::boost INTERFACE IMPORTED GLOBAL)
target_include_directories(Boost::boost SYSTEM INTERFACE ${BOOST_SOURCE})
target_compile_definitions(Boost::boost INTERFACE
    BOOST_ALL_NO_LIB=1
    BOOST_ASIO_DISABLE_BOOST_CONTEXT_FIBER=1
    BOOST_ASIO_DISABLE_BOOST_COROUTINE=1
)
