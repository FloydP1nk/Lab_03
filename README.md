# Лабораторная работа №3 ТиМп
Выполнил Ерохин Павел ИУ8-23
#### Задание 1.
    mkdir formatter_lib
    cd formatter_lib
    mkdir build
    mkdir src
    cd src
    wget https://github.com/tp-labs/lab03/blob/master/formatter_lib/formatter.cpp
    wget https://github.com/tp-labs/lab03/blob/master/formatter_lib/formatter.h
    cd ..
    cat >> CMakeLists.txt <<EOF
      cmake_minimum_required(VERSION 3.22.1 FATAL_ERROR)
      set(CMAKE_CXX_COMPILER "/usr/bin/gcc") 
      project(formatter) 
      set(SOURCE_LIB ~/formatter_lib/src/formatter.cpp ~/formatter_lib/src/formatter.h)
      add_library(mylib STATIC ${SOURCE_LIB})
    EOF
##### Проверка
    cmake ..

![Снимок экрана 2023-03-09 в 01 06 19](https://user-images.githubusercontent.com/113801739/223861670-29d2a28d-318c-4799-82a9-ca0838d76c06.png)
 
 #### Задание 2. 
     mkdir formatter_ex
     cd formatter_exe
     mkdir src
     mkdir build
     cd src
     wget https://github.com/tp-labs/lab03/blob/master/formatter_ex_lib/formatter_ex.h
     wget https://github.com/tp-labs/lab03/blob/master/formatter_ex_lib/formatter_ex.cpp
     cd ..
     cat >> CMakeLists.txt <<EOF
      cmake_minimum_required(VERSION 3.22.1 FATAL_ERROR)
      set(CMAKE_CXX_COMPILER "/usr/bin/gcc") 
      project(formatter) 
      set(SOURCE_LIB ~/formatter_lib/src/formatter.cpp ~/formatter_lib/src/formatter.h)
      add_library(mylib STATIC ${SOURCE_LIB})
    EOF
В файле formatter_ex.cpp указываем путь к файлу formatter.h

      nano formatter_ex.cpp
      #include "~/formatter_lib/src/formatter.h""
    
##### Проверка
    cd build
    cmake ..
    
![Снимок экрана 2023-03-09 в 01 26 20](https://user-images.githubusercontent.com/113801739/223865468-64707e4b-e602-4dad-8ebe-93c48d565088.png)

#### Задание 3. 

##### solver_lib

    cmake_minimum_required(VERSION 3.22.1 FATAL_ERROR)
    project(solver_lib)
    add_library(solver_lib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/solver.cpp)
    add_executable(solver ${CMAKE_CURRENT_SOURCE_DIR}/solver.cpp)
  
##### *hello_world app*

    cmake_minimum_required(VERSION 3.22.1 FATAL_ERROR)
    project(hello_world_app)
    add_executable(hello_world ${CMAKE_CURRENT_SOURCE_DIR}/hello_world.cpp)
    
##### *solver app*

    cmake_minimum_required(VERSION 3.22.1 FATAL_ERROR)
    project(solver_app)
    add_executable(solver_app ${CMAKE_CURRENT_SOURCE_DIR}/equation.cpp)



