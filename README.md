## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [x] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ export GITHUB_USERNAME=SergeyMarti  # Устанавливаем значение переменной окружения GITHUB_USERNAME
$ export GITHUB_EMAIL=sergey.marti33@gmail.com # Устанавливаем значение переменной окружения GITHUB_EMAIL
$ export GITHUB_TOKEN=<сгенирированный_токен> # Устанавливаем значение переменной окружения GITHUB_TOKEN
$ alias edit=subl # Выбираем текстовый редактор
```

```ShellSession
$ cd ${GITHUB_USERNAME}/workspace # Переходим в директорию
$ source scripts/activate # Выполняем скрипт в текущей сессии
```

```ShellSession
$ mkdir ~/.config # Создаем директорию 
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
```

```ShellSession
$ mkdir lab02 && cd lab02 # Создаём директорию и переходим в неё
$ git init # Создаём репозиторий в существующей директории
$ git config --global user.name ${GITHUB_USERNAME} # git config позволяет просматривать и устанавливать параметры; опция --global даёт возможность настроить всего лишь один раз
$ git config --global user.email ${GITHUB_EMAIL} # Указываем имя пользователя и email
$ git config -e --global # Включить поддержку вывода Escape последовательностей;
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02  # Загрузка удаленного репозитория lab02
$ git pull origin master # Выгрузить изменения всех веток с удаленного репозитория в ветку master
$ touch README.md # Создать файл в текущей директории
$ git status # Текущее состояние репозитория (изменения, неразрешенные конфликты)
$ git add README.md # Добавляем новый файл под контроль,чтобы в дальнейшем отслеживать его изменения 
$ git commit -m"added README.md" # Выполняем commit файла и добавляем комментарий к коммиту
$ git push origin master # Залить все изменения ветки master с локального на удаленный репозиторий
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
.idea/
```

```ShellSession
$ git pull origin master # Выгрузить изменения всех веток с удаленного репозитория в ветку master
$ git log # История изменений
```

```ShellSession
$ mkdir sources # Создаем директорий
$ mkdir include
$ mkdir examples

# Запись в .cpp файл участка кода
$ cat > sources/print.cpp <<EOF
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
# end of file — конец файла,переход на новый строку
```

```ShellSession
# Запись в .hpp файл участка кода
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF 
# end of file — конец файла,переход на новый строку
```

```ShellSession
# Запись в .cpp файл участка кода
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
# end of file — конец файла,переход на новый строку
```

```ShellSession
# Запись в .cpp файл участка кода
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
# end of file — конец файла,переход на новый строку
```

```ShellSession
$ edit README.md # Редактируем файл README.md
```

```ShellSession
$ git status # Текущее состояние репозитория
$ git add . # Обработка содержимого текущей директории
$ git commit -m"added sources" # Выполняем commit файла и добавляем комментарий к коммиту
$ git push origin master # Залить все изменения ветки master с локального на удаленный репозиторий
```

## Report

```ShellSession
$ cd ~/workspace/labs/ # Переходим в /workspace/labs/
$ export LAB_NUMBER=02 # Устанавливаем значение переменной окружения LAB_NUMBER
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER} # Клонирование репозитория с лабой
$ mkdir reports/lab${LAB_NUMBER} # Создаем каталог lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md # Копируем README.md в REPORT.md
$ cd reports/lab${LAB_NUMBER} # Меняем директорию на reports/lab${LAB_NUMBER}
$ edit REPORT.md # Редактируем файл REPORT.md
$ gistup -m "lab${LAB_NUMBER}" #Создаем Gist из командной строки и комментарием 
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
4. Добавьте этот файл в локальную копию репозитория.
5. Закоммитьте изменения с *осмысленным* сообщением.
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
8. Запуште изменения в удалёный репозиторий.
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
3. **commit**, **push** локальную ветку в удалённый репозиторий.
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
7. Сделайте *force push* в ветку `patch2`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2019 The ISC Authors
```
