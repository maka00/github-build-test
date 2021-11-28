cmake_minimum_required(VERSION 3.19)
project(app)

set(SOURCES main.cpp)


find_package(Threads)
find_package(PkgConfig REQUIRED)
enable_testing()

if (CMAKE_BUILD_TYPE MATCHES Debug)
    add_definitions(-D_DEBUG=1)
endif ()
add_executable(${PROJECT_NAME} ${SOURCES})

set_target_properties(${PROJECT_NAME}
        PROPERTIES
        DEBUG_POSTFIX "d"
        CXX_STANDARD 20
        )

target_include_directories(${PROJECT_NAME}
        PUBLIC
        ${PROJECT_SOURCE_DIR}

        PRIVATE
        ${CMAKE_CURRENT_BINARY_DIR}

        )
# CMake 3.14 onwards
target_link_directories(${PROJECT_NAME}
        PRIVATE
        ../lib
        )

target_link_libraries(${PROJECT_NAME}
        PUBLIC
        ${CONAN_LIBS}
        Threads::Threads
        )
target_compile_features(${PROJECT_NAME}
        PUBLIC
        cxx_std_17
        )

target_compile_options(${PROJECT_NAME}
        PUBLIC
        PRIVATE
        -Wall -Wextra -pedantic
        )
