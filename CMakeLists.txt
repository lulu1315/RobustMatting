project(RobustMatting)

cmake_minimum_required(VERSION 2.9)
add_compile_options(-std=c++11)

find_package(OpenCV 3.2 REQUIRED)

#installed eigen3 locally : http://eigen.tuxfamily.org/index.php?title=Main_Page
#/usr/local/include/eigen3
find_package(Eigen3 REQUIRED PATHS "/usr/include/eigen3/build")
message(STATUS "Eigen3 found: ${EIGEN3_FOUND}")
message(STATUS "Eigen3 include dir found at ${EIGEN3_INCLUDE_DIR}")
include_directories(${EIGEN3_INCLUDE_DIR})

find_package(OpenMP)
if (OPENMP_FOUND)
    set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    set (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif()

file(GLOB ROBUSTMATTING_SRC
	./src/robust_matting/*.h
	./src/robust_matting/*.cpp
)

add_executable(RobustMatting ${ROBUSTMATTING_SRC})

target_link_libraries(RobustMatting  ${OpenCV_LIBS})
