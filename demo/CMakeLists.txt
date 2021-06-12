cmake_minimum_required(VERSION 3.16)
project(demo VERSION 1.0
        DESCRIPTION "AWS Lambda Posts function"
        LANGUAGES CXX C)

# set everything up for c++17 features
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(aws-lambda-runtime)

add_executable(demo
        src/main.cpp
)

target_include_directories(
  demo PRIVATE
    $<BUILD_INTERFACE:${demo_SOURCE_DIR}/include>
    $<BUILD_INTERFACE:${demo_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)
target_link_libraries(
  demo PRIVATE
    AWS::aws-lambda-runtime 
)
target_compile_features(demo PRIVATE "cxx_std_11")
target_compile_options(demo PRIVATE "-Wall" "-Wextra")

# this line creates a target that packages your binary and zips it up
aws_lambda_package_target(${PROJECT_NAME})
