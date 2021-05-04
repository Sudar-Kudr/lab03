## Laboratory work III


Данная лабораторная работа посвещена изучению систем автоматизации сборки проекта на примере **CMake**



## Tasks

- [ok] 1. Создать публичный репозиторий с названием **lab03** на сервисе **GitHub**
- [ok] 2. Ознакомиться со ссылками учебного материала
- [ok] 3. Выполнить инструкцию учебного материала
- [ok] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**


## Homework

Представьте, что вы стажер в компании "Formatter Inc.".
### Задание 1
Вам поручили перейти на систему автоматизированной сборки **CMake**.
Исходные файлы находятся в директории [formatter_lib](formatter_lib).
В этой директории находятся файлы для статической библиотеки *formatter*.
Создайте `CMakeList.txt` в директории [formatter_lib](formatter_lib),
с помощью которого можно будет собирать статическую библиотеку *formatter*.

1.
 ```sh
$ git clone https://github.com/tp-labs/lab03
```
2. сначала переходим в директорию ```formatter_lib```
``` $ cd formatter_lib```
Создаем и заполняем CmakeList.txt:
```sh
$ cat > CMakeLists.txt <<EOF
> cmake_minimum_required(VERSION 3.4) ---> минимально необходимая версия для работы файлов
> add_library(formatter STATIC formatter.h formatter.cpp) ---> делаем статическую библиотеку из файлов
> EOF
```
3. ```sh $ cmake ~/Sudar-Kudr/workspace/projects/lab03/lab03/formatter_lib/```
4. ```sh $ make```
5. На выходе мы получили файл библиотеки libformatter.a


### Задание 2
У компании "Formatter Inc." есть перспективная библиотека,
которая является расширением предыдущей библиотеки. Т.к. вы уже овладели
навыком созданием `CMakeList.txt` для статической библиотеки *formatter*, ваш 
руководитель поручает заняться созданием `CMakeList.txt` для библиотеки 
*formatter_ex*, которая в свою очередь использует библиотеку *formatter*.

1. Копируем содержимое папки formatter_lib в formatter_ex_lib.
Используем команду:
``` $ cp -r formatter_lib formatter_ex_lib/ ```

2. Создаем и заполняем CmakeList.txt:
```sh
$ cat > CMakeLists.txt <<EOF
> cmake_minimum_required(VERSION 3.4)
> project(formatter_ex)
> include_directories(formatter_lib)
> add_subdirectory(formatter_lib)
> add_library(formatter_ex STATIC formatter_ex.h formatter_ex.cpp)
> target_link_libraries(formatter_ex formatter) 
> EOF
```
3. Запускаем с помощью команды 
``` $ cmake ~/Sudar-Kudr/workspace/projects/lab03/lab03/formatter_ex_lib```
4. ```$ make```
5. На выходе мы получили файл библиотеки libformatter_ex.a

### Задание 3
Конечно же ваша компания предоставляет примеры использования своих библиотек.
Чтобы продемонстрировать как работать с библиотекой *formatter_ex*,
вам необходимо создать два `CMakeList.txt` для двух простых приложений:
* *hello_world*, которое использует библиотеку *formatter_ex*;
* *solver*, приложение которое испольует статические библиотеки *formatter_ex* и *solver_lib*.

* *1. Сначала переместим formatter_ex_lib в папку с hello_world_application.
Команда:
```$ mv formatter_ex_lib/ hello_world_application/```
2. Спускаемся в hello_world_application 
``` $ cd hello_world_application```
Создаем и заполняем CmakeList.txt:
```sh
cat > CMakeLists.txt <<EOF
> cmake_minimum_required(VERSION 3.4)
> project(hello_world)
> include_directories(formatter_ex_lib)
> add_subdirectory(formatter_ex_lib)
> add_executable(hello_world hello_world.cpp)
> target_link_libraries(hello_world formatter_ex)
> EOF 
```
3. Запускаем... 
``` $ cmake ~/Sudar-Kudr/workspace/projects/lab03/lab03/hello_world_application```
4. ```$ make```
5. В директории hello_world_application появился файл hello_world


* *Необходимо создать CmakeList.txt для solver_lib и solver_application
1. сначала переходим в папку solver_lib
```sh
$ cd ..
$ ls
CMakeLists.txt    formatter_lib            solver_application
LICENSE           hello_world_application  solver_lib
README.md         preview.png
$ cd solver_lib/
```
2. Создание CMakeLists.txt для solver_lib:
```sh
cat > CMakeLists.txt <<EOF
> cmake_minimum_required(VERSION 3.4) 
> add_library(solver_lib STATIC solver.h solver.cpp)
> EOF
```
3. переходим в папку solver_application
```sh
$ cd ..
$ ls
CMakeLists.txt   formatter_lib             solver_application
LICENSE          hello_world_application   solver_lib
README.md        preview.png
$ cd solver_application/
```
И создаем CMakeLists.txt для solver_application:
```sh
cat > CMakeLists.txt <<EOF
> cmake_minimum_required(VERSION 3.4)
> project(solver)
> add_executable(solver equation.cpp)
> include_directories(formatter_ex_lib)
> add_subdirectory(formatter_ex_lib)
> include_directories(solver_lib)
> add_subdirectory(solver_lib)
> target_link_libraries(solver formatter_ex)
> target_link_libraries(solver solver_lib)
> EOF
```

3. Сначала нужно перемести formatter_ex_lib из hello_world_application в solver_application...
```sh
$ cd ..                                     (возвращаемся в lab03/)
$ cd hello_world_application/               (входим...)
$ mv formatter_ex_lib/ ..                   (вернулась в lab03/)
$ cd ..                                     (возвращаемся в lab03/)
$ mv formatter_ex_lib/ solver_application/  (ух)
```
Теперь переместим solver_lib в solver_application
```$ mv solver_lib/ solver_application/```
Спускаемся в solver_application 
``` $ cd solver_application```

4. Повторяем те же команды: сборка, запуск...
```sh
$ cmake ~/Sudar-Kudr/workspace/projects/lab03/lab03/solver_application
$ make
```
5. После использовании команды make выяснилось, что в файле solver.cpp в папке solver_lib есть ошибки...
исправляем... 
Заменим в строке ```throw std::logic_error{"error: discriminant < 0"};``` кривые скобки на ```(``` и ```)```,
там, где присваиваем значения ```x1``` и ```x2``` заменим ```sqrtf```на ```sqrt```, а также дописали библиотеку ```#include <cmath>```.


6. Проверяем ``` $ make```
7. Все стало хорошо и появился файл solver
8. Запускаем... 
```$ ./solver```
введем данные
```sh
4
3
1
```
получим выход:
```sh
-------------------------
error: discriminant < 0
-------------------------
```


```
Copyright (c) 2015-2021 The ISC Authors
```
