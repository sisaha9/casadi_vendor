cmake_minimum_required(VERSION 3.10)
project(casadi_vendor CXX)

find_package(ament_cmake REQUIRED)
find_package(ament_cmake_vendor_package REQUIRED)
find_package(casadi 3.6.3 QUIET)

ament_vendor(casadi_vendor
  SATISFIED ${casadi_FOUND}
  VCS_URL https://github.com/casadi/casadi.git
  VCS_VERSION 3.6.3
  CMAKE_ARGS
    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
    -DWITH_IPOPT=ON:BOOL=ON
    -DWITH_OSQP=ON:BOOL=ON
    -DWITH_QPOASES=ON:BOOL=ON
    -DWITH_LAPACK=ON:BOOL=ON
    -DWITH_SLICOT=ON:BOOL=ON
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  list(APPEND AMENT_LINT_AUTO_EXCLUDE
    ament_cmake_cppcheck
  )
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()