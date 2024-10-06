cmake_minimum_required(VERSION 3.20)
project(GitHubDockerTest)

# C++ Language standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_executable(GitHubDockerTest
    src/Main.cpp
)
install(TARGETS GitHubDockerTest DESTINATION bin)