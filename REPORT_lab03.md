## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [ok] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [ok] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [ok] 3. Ознакомиться со ссылками учебного материала
- [ok] 4. Выполнить инструкцию учебного материала
- [ok] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=<имя_пользователя>    #присваиваем <имя_пользователя> в переменную GITHUB_USERNAME
```

```sh
$ cd ${GITHUB_USERNAME}/workspace    #спускаемся в workspace
$ pushd .                            #добавляем в стек текущий каталог
$ source scripts/activate            #выполняем скрипт
```

```sh
$ git clone https://github.com/${GITHUB_USERNAME}/lab02.git projects/lab03        #клонируем репозиторий с прошлой лабораторной (lab02) в папку lab03
$ cd projects/lab03                                                             #спускаемся в папку lab03
$ git remote remove origin                                                    #удаление старой ссылки репозитория с lab02
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab03.git     #добавление новой ссылки удалённого репозитория
```

```sh
$ g++ -std=c++11 -I./include -c sources/print.cpp       #устанавливаем версию С++ и cобираем файл print.cpp
$ ls print.o                                            #выводим файлы, которые появились после компиляции файла print.o
$ nm print.o | grep print                               #выводим список символов из объектного файла print.
$ ar rvs print.a print.o                                #создаем архив print.a из файла print.o
$ file print.a                                          #узнаем тип данных
$ g++ -std=c++11 -I./include -c examples/example1.cpp   #устанавливаем версию С++ и cобираем файл example1.cpp
$ ls example1.o                                         #выводим файлы, которые появились после компиляции файла example1.o
$ g++ example1.o print.a -o example1                    #запускаем код в example1.o и print.a, указываем имя исполняемого файла, который получим на выходе (example1)
$ ./example1 && echo                                    #запускаем файл и выводим содержимое
```

```sh
$ g++ -std=c++11 -I./include -c examples/example2.cpp   #устанавливаем версию С++ и cобираем файл example2.cpp
$ nm example2.o                                         #выводим список символов из объектного файла example2.o
$ g++ example2.o print.a -o example2                    #запускаем код в example2.o и print.a, указываем имя исполняемого файла, который получим на выходе (example2)
$ ./example2                                            #запускаем файл
$ cat log.txt && echo                                   #считываем файл log.txt выводим его содержимое
```

```sh
$ rm -rf example1.o example2.o print.o                  #удаляем файлы rm -rf example1.o, example2.o и print.o
$ rm -rf print.a                                        #удаляем файл print.a
$ rm -rf example1 example2                              #удаляем программу example1 и example2
$ rm -rf log.txt                                        #удаляем файл log.txt
```

```sh
$ cat > CMakeLists.txt <<EOF                            #открываем файл и пишем данные от EOF до EOF
cmake_minimum_required(VERSION 3.4)
project(print)
EOF
```

```sh
$ cat >> CMakeLists.txt <<EOF                           #открываем файл и продолжаем писать данные от EOF до EOF
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
EOF
```

```sh
$ cat >> CMakeLists.txt <<EOF                            #открываем файл и продолжаем писать данные от EOF до EOF
add_library(print STATIC \${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
EOF
```

```sh
$ cat >> CMakeLists.txt <<EOF                           #открываем файл и продолжаем писать данные от EOF до EOF
include_directories(\${CMAKE_CURRENT_SOURCE_DIR}/include)
EOF
```

```sh
$ cmake -H. -B_build             #устанавливаем в директорию _build файлы сборки
$ cmake --build _build           #запускаем сборку
```

```sh
$ cat >> CMakeLists.txt <<EOF           #открываем файл и продолжаем писать данные от EOF до EOF

add_executable(example1 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
add_executable(example2 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
EOF
```

```sh
$ cat >> CMakeLists.txt <<EOF           #открываем файл и продолжаем писать данные от EOF до EOF

target_link_libraries(example1 print)
target_link_libraries(example2 print)
EOF
```

```sh
$ cmake --build _build                          #запускаем сборку
$ cmake --build _build --target print           #запускаем сборку print
$ cmake --build _build --target example1        #запускаем сборку example1
$ cmake --build _build --target example2        #запускаем сборку example2
```

```sh
$ ls -la _build/libprint.a       #выводим информацию о файле _build
$ _build/example1 && echo        #запускаем файл и выводим содержимое
hello
$ _build/example2                #запускаем файл
$ cat log.txt && echo            #считываем файл log.txt выводим его содержимое
hello
$ rm -rf log.txt                 #удаляем файл log.txt
```

```sh
$ git clone https://github.com/tp-labs/lab03 tmp       #клонируем репозиторий по ссылке в директорию tmp
$ mv -f tmp/CMakeLists.txt .                         #перемещаем файл CmakeList.txt в директорию tmp
$ rm -rf tmp                                       #удаляем папку tmp
```

```sh
$ cat CMakeLists.txt                                       #выводим данные файла CMakeList.txt
$ cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install     #устанавливаем префикс на _install
$ cmake --build _build --target install                #запускаем сборку install
$ tree _install                                      #выводим в терминал структуру папки _install, в виде "дерева"
```

```sh
$ git add CMakeLists.txt                    #добавляем CMakeLists.txt
$ git commit -m "added CMakeLists.txt"    #закомментируем его
$ git push origin main                  #отправляем данные на сервер, в удаленный репозиторий main
```

## Report

```sh
$ popd
$ cd ~/workspace/                                                                #переходим в папку workspace
$ export LAB_NUMBER=03                                                          #присваиваем 03 в переменную LAB_NUMBER
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER} #клонируем из ссылки в директорию (в наше случае-tasks/lab03)
$ mkdir reports/lab${LAB_NUMBER}                                              #создаем директорию (в наше случае- lab03)                                      
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md     #спускаемся в директорию (в наше случае- lab03)
$ cd reports/lab${LAB_NUMBER}                                               #копируем из одной директории в другую
$ edit REPORT.md                                                           #редактируем REPORT.md
$ gist REPORT.md                                                          #сохраняем REPORT.md
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
`Репозиторий с названием lab02 был выполнен`
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
`Инструкция была выполнена`
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.

```sh
cat > sources/hello_world.cpp <<EOF
#include <iostream>
#include <iostream>

using namespace std;

int main()
{
    cout<<"Hello World";

    return 0;
}
EOF
```
4. Добавьте этот файл в локальную копию репозитория.
`$ git add sources/hello_world.cpp`
5. Закоммитьте изменения с *осмысленным* сообщением.
`$ git commit -m "файл Привет мир в cpp"`
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
```sh
Вызываем команду которая даст нам изменить код
$ edit sources/hello_world.cpp
Делаем изменения...
```
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
git add sources/hello_world.cpp
`Не добавляем повторно, потому что мы не создаем новый файл и до этого мы не пушили изменения`
`$ git commit -m "Изменен файл Привет мир в cpp"`
8. Запуште изменения в удалёный репозиторий.
`$ git push`
9. Проверьте, что история коммитов доступна в удалёный репозитории.
`В GitHub появился файл с последним добавленным коммитом и видно изменения файла (до и после).`

### Part II

1. В локальной копии репозитория создайте локальную ветку `patch1`.
`$ git checkout -b patch1`
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
`$ edit hello_world.cpp`
`$ git add hello_world.cpp`
3. **commit**, **push** локальную ветку в удалённый репозиторий.
```sh
$ git commit -m "Избавил от namespace"
$ git push
```
`Произошла ошибка, исправляем...`
```sh
$ git push —set-upstream origin patch1
$ git push
```
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
`$ git status`
5. Создайте pull-request `patch1 -> master`.
`Создано`
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
`$ edit hello_world.cpp`
`$ git add hello_world.cpp`
7. **commit**, **push**.
`$ git commit -m "Изменен опять.."`
`$ git push`
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
`Проверил, что новые изменения есть`
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
```sh
$ git checkout main
$ git merge patch1
$ git branch -d patch1
$ git push origin --delete patch1
```
10. Локально выполните **pull**.
`$ git pull`
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
`$ git log`
```sh
commit 227cbc669e2ea78ee446af4659815660970e25e5 (HEAD -> main)
Author: Sudar-Kudr <melihovivan936@gmail.com>
Date:   Mon Mar 29 22:43:11 2021 +0300

    Изменен опять..

commit 276ec4454b307b71d0c7237a2c815fe062090744 (origin/main)
Author: Sudar-Kudr <melihovivan936@gmail.com>
Date:   Sun Mar 28 15:59:33 2021 +0300

    Изменен файл Привет мир в cpp

commit 429781b5021f1a779f8f16833d7dcda504383fed
Author: Sudar-Kudr <melihovivan936@gmail.com>
Date:   Sun Mar 28 15:50:02 2021 +0300

    added sources+

commit c6811360ef2f46e66d7a90d8d423608d6fd0c917
Author: Sudar-Kudr <melihovivan936@gmail.com>
Date:   Sun Mar 28 15:45:53 2021 +0300

    файл Привет мир в cpp
```
12. Удалите локальную ветку `patch1`.
`$ git branch -d patch1`
### Part III

1. Создайте новую локальную ветку `patch2`.
`$ git checkout -b patch2`
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
`$ clang-format -style=Mozilla hello_world.cpp`
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
```sh
$ edit hello_world.cpp
$ git add hello_world.cpp
$ git commit -m "Стиль изменен"
$ git push
$ git push --set-upstream origin patch2
```
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
`Изменил комментарии`
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
```sh
$ git checkout patch2
$ git pull origin main
$ git rebase main
$ git add hello_world.cpp
$ git commit -m "Исправил конфликт"
$ git rebase main
```
7. Сделайте *force push* в ветку `patch2`
`$ git push origin patch2 —force`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.
```sh
$ git checkout main
$ git merge patch2
$ git push
```
