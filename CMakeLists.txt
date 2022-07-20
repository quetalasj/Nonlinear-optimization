cmake_minimum_required(VERSION 3.22)
project(Nonlinear_optimization)

set(CMAKE_CXX_STANDARD 17)

list(APPEND CMAKE_MODULE_PATH /home/evgeny/g2o/cmake_modules)
message("${CMAKE_MODULE_PATH} == CMAKE_MODULE_PATH")
find_package(OpenCV REQUIRED)
find_package(Sophus REQUIRED)
find_package(Pangolin REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(Ceres REQUIRED)
find_package(G2O MODULE REQUIRED)

message("G2O_ROOT: ${G2O_ROOT}")
message("G2O_INCLUDE_DIR: ${G2O_INCLUDE_DIR}")
message("G2O_SOLVERS_FOUND: ${G2O_SOLVERS_FOUND}")
message("G2O_FOUND: ${G2O_FOUND}")

include_directories(${OpenCV_INCLUDE_DIRS})
include_directories("/usr/include/eigen3")
include_directories(${Sophus_INCLUDE_DIRS})
include_directories(${G2O_INCLUDE_DIRS})


add_executable(gaussNewton gaussNewton.cpp)
add_executable(ceresCurveFitting ceresCurveFitting.cpp)
add_executable(g2oCurveFitting g2oCurveFitting.cpp)

target_link_libraries(gaussNewton ${OpenCV_LIBS} ${Pangolin_LIBRARIES} Sophus::Sophus Eigen3::Eigen)
target_link_libraries(ceresCurveFitting ${OpenCV_LIBS} Ceres::ceres)


target_link_libraries(g2oCurveFitting ${G2O_CORE_LIBRARY} ${G2O_STUFF_LIBRARY} ${OpenCV_LIBS} Eigen3::Eigen Ceres::ceres)
