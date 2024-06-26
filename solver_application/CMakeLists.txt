cmake_minimum_required(VERSION 3.29)
project(solver)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CURRENT_SOURCE_DIR /Users/mihailerosenko/z1qnezt/workspace/tasks/lab03)

# Добавляем директиву include_directories для поиска заголовочных файлов
include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib
    ${CMAKE_CURRENT_SOURCE_DIR}/formatter_lib
    ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib
)

# Создаем библиотеку solver_lib
add_library(solver_lib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib/solver.cpp)

# Создаем исполняемый файл solver и связываем его с библиотеками
add_executable(solver ${CMAKE_CURRENT_SOURCE_DIR}/solver_application/equation.cpp)

# Ищем библиотеки formatter, formatter_ex, и solver_lib
find_library(formatter NAMES libformatter.a PATHS ${CMAKE_CURRENT_SOURCE_DIR}/formatter_lib)
find_library(formatter_ex NAMES libformatter_ex.a PATHS ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib)
find_library(solver_lib NAMES libsolver.a PATHS ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib)

# Связываем исполняемый файл с библиотеками
target_link_libraries(solver ${formatter} ${formatter_ex} ${solver_lib})
