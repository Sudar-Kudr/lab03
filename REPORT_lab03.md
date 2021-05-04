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
