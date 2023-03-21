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
      project(formatter_lib) 
      set(CMAKE_CXX_STANDARD 11)
      set(CMAKE_CXX_STANDARD_REQUIRED ON)
      add_library(formatter_lib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/src/formatter.cpp)
    EOF
##### Проверка
    cmake ..
    
![Снимок экрана 2023-03-09 в 01 06 19](https://user-images.githubusercontent.com/113801739/223861670-29d2a28d-318c-4799-82a9-ca0838d76c06.png)

        cmalke --build .
 
<img width="402" alt="Снимок экрана 2023-03-09 в 12 17 50" src="https://user-images.githubusercontent.com/113801739/223976598-41a669c3-e5ac-4737-b5c1-033ed474f32e.png">


 #### Задание 2. 
     mkdir formatter_ex_lib
     cd formatter_ex
     mkdir src
     mkdir build
     cd src
     wget https://github.com/tp-labs/lab03/blob/master/formatter_ex_lib/formatter_ex.h
     wget https://github.com/tp-labs/lab03/blob/master/formatter_ex_lib/formatter_ex.cpp
     cd ..
     cat >> CMakeLists.txt <<EOF
        cmake_minimum_required(VERSION 3.4)
        project(formatter_ex)
        set(CMAKE_CXX_STANDARD 11)
        set(CMAKE_CXX_STANDARD_REQUIRED ON)
        include_directories("~/formatter_lib/src")
        add_library(formatter_exlib STATIC ~/formatter_ex/src/formatter_ex.cpp ~/formatter_ex/src/formatter_ex.h)
        add_executable(formatter_ex ~/formatter_ex/src/formatter_ex.cpp)
        target_link_libraries(formatter_ex formatter_exlib)
    EOF

    
##### Проверка
    cd build
    cmake ..
    
![Снимок экрана 2023-03-09 в 01 26 20](https://user-images.githubusercontent.com/113801739/223865468-64707e4b-e602-4dad-8ebe-93c48d565088.png)

    cmake --build .
    
![Снимок экрана 2023-03-21 в 22 37 21](https://user-images.githubusercontent.com/113801739/226722299-0c81dfdf-3c2a-465b-819d-51f66faa66f0.png)


#### Задание 3. 

##### solver_lib

    cmake_minimum_required(VERSION 3.22.1 FATAL_ERROR)
    project(solver_lib)
    add_library(solver_lib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/solver.cpp)
    add_executable(solver ${CMAKE_CURRENT_SOURCE_DIR}/solver.cpp)
  
##### *hello_world app*

    cmake_minimum_required(VERSION 3.22.1 FATAL_ERROR)
    project(hello_world)
    include_directories("~/formatter_lib/src")
    include_directories("~/formatter_ex_lib/src")
    add_library(formatter_lib STATIC "~/formatter_lib/src/formatter.cpp")
    add_library(formatter_ex_lib STATIC "~/formatter_ex_lib/src/formatter_ex.cpp")
    add_executable(hello_exec "~/hello_world/src/hello_world.cpp")
    target_link_libraries(hello_exec formatter_lib formatter_ex_lib)
   

![hello_world_1](https://user-images.githubusercontent.com/113801739/226726898-25f06ade-674b-457f-a05a-09c51a47a9da.png)

    cd build 
    ./hello_exec
    
![hello_world_2](https://user-images.githubusercontent.com/113801739/226727131-91fdf858-87ea-40e2-9249-b4c4993be9a9.png)


    
##### *solver app*

    cmake_minimum_required(VERSION 3.4)
    project(solver)
    set(CMAKE_CXX_STANDARD 11)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib formatter_ex_lib_dir)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib solver_lib_dir)
    add_executable(solver ${CMAKE_CURRENT_SOURCE_DIR}/src/equation.cpp)
    target_include_directories(formatter_ex_lib PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib/src
    ${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib/src
    )
    target_link_libraries(solver formatter_ex_lib solver_lib)

![Снимок экрана 2023-03-22 в 01 03 39](https://user-images.githubusercontent.com/113801739/226752262-41683fb7-68b6-4264-a483-bcfccdbb18fa.png)

![Снимок экрана 2023-03-22 в 01 03 53](https://user-images.githubusercontent.com/113801739/226752280-f45d7a2c-641a-4259-a9af-8533f1a8acff.png)

