set(CXXLIB "cnutil")

find_package(Boost COMPONENTS thread system program_options date_time filesystem REQUIRED)

# Flags
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -D_GNU_SOURCE")

include_directories(${Boost_INCLUDE_DIRS})
include_directories("${MONERO_DIR}/contrib/epee/include")
include_directories("${MONERO_DIR}/external/easylogging++")
include_directories("${MONERO_DIR}/src")

link_directories(
    ${MONERO_DIR}/src/cryptonote_core
    ${MONERO_DIR}/src/crypto
    ${MONERO_DIR}/src/common
    ${MONERO_DIR}/src/ringct
)

# Build library
add_library(${CXXLIB} SHARED src/cnutil.cpp)

target_link_libraries(${CXXLIB}
    cryptonote_core
    crypto
    common
    ringct
)

target_link_libraries(${CXXLIB}
    ${Boost_THREAD_LIBRARY}
    ${Boost_SYSTEM_LIBRARY}
    ${Boost_PROGRAM_OPTIONS_LIBRARY}
    ${Boost_DATE_TIME_LIBRARY}
    ${Boost_FILESYSTEM_LIBRARY}
)
