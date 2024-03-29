cmake_minimum_required(VERSION 3.2)
project(KMCUDA)

add_compile_options(-std=c++11)
SET(CMAKE_BUILD_TYPE Release)

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)

find_package(OpenMP REQUIRED)

find_package(CUDA QUIET REQUIRED)

# if (PROFILE OR CMAKE_BUILD_TYPE STREQUAL "Debug")
#   set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DPROFILE")
# endif()

#set(CMAKE_VERBOSE_MAKEFILE on)

if (NOT DEFINED CUDA_ARCH)
  set(CUDA_ARCH "61")
endif()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -march=native -Wall -Werror -DCUDA_ARCH=${CUDA_ARCH} -std=c++11 ${OpenMP_CXX_FLAGS}")

set(SOURCE_FILES kmcuda.cc kmcuda.h wrappers.h private.h fp_abstraction.h tricks.cuh
                 metric_abstraction.h kmeans.cu knn.cu transpose.cu)

# if (CMAKE_BUILD_TYPE STREQUAL "Debug")
#   set(NVCC_FLAGS "-G -g")
# endif()

set(CUDA_NVCC_FLAGS "${CUDA_NVCC_FLAGS} -arch sm_${CUDA_ARCH} -Xptxas=-v -D_MWAITXINTRIN_H_INCLUDED -D_FORCE_INLINES")

if (CMAKE_MAJOR_VERSION LESS 4 AND CMAKE_MINOR_VERSION LESS 3)
  # workaround https://github.com/Kitware/CMake/commit/99abebdea01b9ef73e091db5594553f7b1694a1b
  message(STATUS "Applied CUDA C++11 workaround on CMake < 3.3")
  set(CUDA_NVCC_FLAGS "${CUDA_NVCC_FLAGS} --std c++11")
endif()

cuda_add_library(KMCUDA SHARED ${SOURCE_FILES} OPTIONS ${NVCC_FLAGS})

target_link_libraries(KMCUDA ${CUDA_curand_LIBRARY}    ${CUDA_LIBRARIES})



