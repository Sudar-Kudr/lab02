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
$ export GITHUB_USERNAME=<имя_пользователя>        #присваиваем имя пользователя GitHub в переменную GITHUB_USERNAME
$ export GITHUB_EMAIL=<адрес_почтового_ящика>     #присваиваем адрес почты в переменную GITHUB_EMAIL
$ export GITHUB_TOKEN=<сгенирированный_токен>    #присваиваем сгенирированный токен в переменную GITHUB_TOKEN
$ alias edit=<nano|vi|vim|subl>                 #выбираем какой редактор хотим открыть
```

```sh
$ cd ${GITHUB_USERNAME}/workspace   #спускаемся в workspace
$ source scripts/activate          #выполняем скрипт
```

```sh
$ mkdir ~/.config                              #создаем директорию .config
$ cat > ~/.config/hub <<EOF                   #создаем файл и пишем данные от EOF до EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https    #задаем https протокол
```

```sh
$ mkdir projects/lab02 && cd projects/lab02                        #создаем в директории projects папку lab02 и спускаемся в неё
$ git init                                                          #создаём подкаталог с именем .git, содержащий структуру git репозитория
$ git config --global user.name ${GITHUB_USERNAME}                   #указываем имя пользователя 
$ git config --global user.email ${GITHUB_EMAIL}                      #указываем адрес адрес почтового ящика
# check your git global settings                                       #(пер.) проверьте глобальные настройки git
$ git config -e --global                                                #показывает глобальную конфигурацию.
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git  #добавление удалённого репозитория
$ git pull origin main                                                  #забираем изменения из удаленного репозитория и проведем слияние с веткой main
$ touch README.md                                                      #создаем файл README.md
$ git status                                                          #проверяем состояние репозитория
$ git add README.md                                                  #добавляем файл
$ git commit -m "added README.md"                                   #закомментируем все файлы, в которых были изменения
$ git push origin main                                             #отправляем данные на сервер, в удаленный репозиторий main
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```sh
*build*/
*install*/
*.swp
.idea/
```

```sh
$ git pull origin main     #забираем изменения из удаленного репозитория и проведем слияние с веткой main
$ git log                  #посмотрим истории коммитов
```

```sh
$ mkdir sources                #создаем папку sourses
$ mkdir include                 #создаем папку include
$ mkdir examples                 #создаем папку examples
$ cat > sources/print.cpp <<EOF   #создаем файл формата .cpp и пишем данные от EOF до EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```sh
$ cat > include/print.hpp <<EOF           #создаем файл формата .hpp и пишем данные от EOF до EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```sh
$ cat > examples/example1.cpp <<EOF        #создаем файл формата .cpp и пишем данные от EOF до EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```sh
$ cat > examples/example2.cpp <<EOF        #создаем файл формата .cpp и пишем данные от EOF до EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```sh
$ edit README.md     #открываем текстовый редактор и редактируем README.md
```

```sh
$ git status                   #проверяем состояние репозитория
$ git add .                     #добавляем все файлы, в которых были изменения
$ git commit -m"added sources"   #закомментируем все файлы, в которых были изменения
$ git push origin master          #отправляем данные на сервер, в удаленный репозиторий main
```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=02                                                          #присваиваем 02 в переменную LAB_NUMBER
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER} #клонируем из ссылки в директорию (в наше случае-tasks/lab02)
$ mkdir reports/lab${LAB_NUMBER}                                              #создаем в директории reports папку (в нашем случае- lab02)                                      
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md     #спускаемся в директорию (в наше случае- lab02)
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
