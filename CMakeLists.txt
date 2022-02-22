cmake_minimum_required(VERSION 3.14)

project(exceptionperformance CXX)

add_executable(runtests
    main.cpp
    exceptions.cpp
    leaf.cpp
    expected.cpp
    herbceptionemulation.cpp
    herbceptions.cpp
    outcome.cpp
    baseline.cpp
)

target_compile_features(runtests PRIVATE cxx_std_20)

find_package(benchmark)

if(NOT benchmark_FOUND)
    set(BENCHMARK_ENABLE_TESTING OFF)
    set(BENCHMARK_ENABLE_INSTALL OFF)
    set(BENCHMARK_ENABLE_GTEST_TESTS OFF)

    include(FetchContent)

    FetchContent_Declare(benchmark
        URL https://github.com/google/benchmark/archive/refs/tags/v1.6.1.zip
        URL_HASH SHA256=367e963b8620080aff8c831e24751852cffd1f74ea40f25d9cc1b667a9dd5e45
        SOURCE_DIR benchmark
    )

    FetchContent_MakeAvailable(benchmark)
endif()

add_executable(runtests_googlebenchmark
    main_googlebench.cpp
    exceptions.cpp
    # leaf.cpp
    # expected.cpp
    # herbceptionemulation.cpp
    # herbceptions.cpp
    # outcome.cpp
    baseline.cpp
)

target_compile_features(runtests_googlebenchmark PRIVATE cxx_std_20)

target_link_libraries(runtests_googlebenchmark benchmark::benchmark)
