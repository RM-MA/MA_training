cmake_minimum_required(VERSION 3.15)

project(MA)

## PROJECT_DIR这个量，就可以在代码中使用
add_compile_definitions(PROJECT_DIR="${PROJECT_SOURCE_DIR}")

## Set the basic info for project
<<<<<<< HEAD
=======

if(NOT CXX_STANDARD)
    set(CXX_STANDARD_REQUIRED ON)
    set(CXX_STANDARD 20)
endif()

>>>>>>> 21002ca (Add some openvino demo)
set(SRC_LIST orb_cv.cpp)
set(2D_2D pose_estimation_2d_to_2d.cpp)
set(KALMAN kalman_filter.cpp)
set(EKF EKF.cpp)
<<<<<<< HEAD
<<<<<<< HEAD
=======
set(TEST test.cpp)
>>>>>>> b4fbe88 (Add deep learning demo)
=======
set(TS test.cpp)
>>>>>>> 21002ca (Add some openvino demo)

## Export compile commands for clangd
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

## By adding -Wall and -Werror, the complier does not ignore warnings
## enforcing cleaner code
add_definitions(-Wall -Werror)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)

find_package(Eigen3 REQUIRED)

include_directories(${EIGEN3_INCLUDE_DIR})


message(STATUS "Current binary working dir is " ${PROJECT_BINARY_DIR})
message(STATUS "Current source working dir is " ${PROJECT_SOURCE_DIR})

<<<<<<< HEAD
<<<<<<< HEAD
add_executable(${PROJECT_NAME} ${EKF})
=======
add_executable(${PROJECT_NAME} ${EKF})
add_executable(TE ${TS})
>>>>>>> 21002ca (Add some openvino demo)

include_directories(modules)
add_subdirectory(modules)
target_link_libraries(MA modules)
<<<<<<< HEAD
=======
# add_executable(${PROJECT_NAME} ${EKF})
add_executable(T ${TEST})

include_directories(modules)
add_subdirectory(modules)
target_link_libraries(T modules)
>>>>>>> b4fbe88 (Add deep learning demo)
=======
>>>>>>> 21002ca (Add some openvino demo)
