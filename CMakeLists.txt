cmake_minimum_required(VERSION 3.11)

include(FetchContent)
FetchContent_Declare(
  pcl
  URL https://github.com/PointCloudLibrary/pcl/archive/refs/tags/pcl-1.6.0.tar.gz
  URL_HASH SHA256=9d444063fe84a5bb677143af7db59e612511055678531d09daca0b6b622595bb
)

FetchContent_GetProperties(pcl)
if(NOT pcl_POPULATED)
  FetchContent_Populate(pcl)
  set(CMAKE_MODULE_PATH ${pcl_SOURCE_DIR}/cmake/Modules)
  set(CMAKE_BUILD_TYPE Release)
  set(CMAKE_CONFIGURATION_TYPES Release)
  set(CMAKE_INSTALL_PREFIX ${CMAKE_CURRENT_LIST_DIR}/install)
  
  set(BOOST_ROOT ${CMAKE_CURRENT_LIST_DIR}/3rdParty/Boost)
  set(EIGEN_ROOT ${CMAKE_CURRENT_LIST_DIR}/3rdParty/Eigen)
  set(FLANN_ROOT ${CMAKE_CURRENT_LIST_DIR}/3rdParty/FLANN)
  set(QHULL_ROOT ${CMAKE_CURRENT_LIST_DIR}/3rdParty/Qhull)
  
  file(COPY ${CMAKE_CURRENT_LIST_DIR}/eigen.h
       DESTINATION ${pcl_SOURCE_DIR}/common/include/pcl/common)
  file(COPY ${CMAKE_CURRENT_LIST_DIR}/kdtree_flann.h 
       DESTINATION ${pcl_SOURCE_DIR}/kdtree/include/pcl/kdtree)
  file(COPY ${CMAKE_CURRENT_LIST_DIR}/ply_parser.h 
       DESTINATION ${pcl_SOURCE_DIR}/io/include/pcl/io/ply)
  file(COPY ${CMAKE_CURRENT_LIST_DIR}/PCLConfig.cmake.in 
       DESTINATION ${pcl_SOURCE_DIR})
  
  add_definitions(-D_SILENCE_STDEXT_HASH_DEPRECATION_WARNINGS)
  add_subdirectory(${pcl_SOURCE_DIR} ${pcl_BINARY_DIR})
endif()
