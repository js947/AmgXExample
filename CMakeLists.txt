CMAKE_MINIMUM_REQUIRED(VERSION 3.17)
PROJECT(example_poisson C CXX)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")

add_executable(poisson
    main.cpp
    createKSP.cpp
    factories.cpp
    io.cpp
    solve.cpp
    StructArgs.cpp
    fixSingularMat.cpp
    )

find_package(AmgXWrapper REQUIRED)
target_link_libraries(poisson PUBLIC AmgXWrapper)

set(CMAKE_SKIP_BUILD_RPATH FALSE)
set(CMAKE_BUILD_WITH_INSTALL_RPATH FALSE)
set(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib;${CMAKE_INSTALL_PREFIX}/lib64")
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

list(FIND CMAKE_PLATFORM_IMPLICIT_LINK_DIRECTORIES "${CMAKE_INSTALL_PREFIX}/lib" isSystemDir)
if("${isSystemDir}" STREQUAL "-1")
  set(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")
endif("${isSystemDir}" STREQUAL "-1")


install(TARGETS poisson DESTINATION "bin")
