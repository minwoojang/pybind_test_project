# 최소 CMake 버전 지정
cmake_minimum_required(VERSION 3.10)

# 프로젝트 이름과 버전 지정
project(example LANGUAGES CXX)

# C++ 표준 설정
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Python 3을 찾기 위한 설정
find_package(Python3 REQUIRED COMPONENTS Interpreter Development)

# Python 관련 경로 지정 (필요한 경우 경로를 명시적으로 설정)
include_directories(${Python3_INCLUDE_DIRS})
link_directories(${Python3_LIBRARY_DIRS})

# pybind11 설정 (pybind11 설치 경로 지정)
include_directories("/cocoa/inhouse/tool/rez-packages/pybind11/2.4.2/include")

# 소스 파일 추가
add_library(example MODULE example.cpp)

# pybind11 라이브러리 링크
target_link_libraries(example PRIVATE ${Python3_LIBRARIES})

# Python 인터프리터와 pybind11 모듈 연결
target_link_libraries(example PRIVATE Python3::Python)

