Laboratory work III

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab03** и с лиценцией **MIT**
- [ ] 2. Ознакомиться со ссылками учебного материала
- [ ] 3. Выполнить инструкцию учебного материала
- [ ] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ export GITHUB_USERNAME=<имя_пользователя>
Команда присвоила GITHUB_USERNAME , то значение, которое мы ввели.
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
Команда присвоила GITHUB_EMAIL, то значение почтового ящика, которое мы ввели.
$ alias edit=<nano|vi|vim|subl>
Команда создала синоним edit для команды vim. То есть когда мы набираем edit, то по сути вызываем vim или другой текстовый редактор.
```

```ShellSession
$ cd ${GITHUB_USERNAME}/workspace
Команда cd перемещает нас в директорию {GITHUB_USERNAME}/workspace.
$ source scripts/activate
Команда source читает и выполняет команды из файла с именем scripts/activate в текущем окружении.
```

```ShellSession
$ mkdir projects/lab03 && cd projects/lab03
Создает папку projects/lab03 и в тоже время перемещает нас в нее.
$ git init
Initialized empty Git repository in /home/ubuntu/workspace/git/AlexDeveloper24/workspace/projects/lab03/.git/
Инициализирует пустой git репозиторий в указанной папке.
$ git config --global user.name ${GITHUB_USERNAME}
С помощью команд git config устанавливаем пользовательские параметры. Этой командой устанавливаем имя пользователя.
$ git config --global user.email ${GITHUB_EMAIL}
Устававливаем email адрес пользователя. Опция --global означает, что эти параметры будут применяться для всех проетов.
$ git config -e --global
Открывает редактор по умолчанию, позволяет просмотреть и изменить данные пользователя и некоторые настройки.
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab03.git
Команда добавляет удаленный репозиторий с именем origin.
$ git pull origin master
Команда git pull автоматически получает изменения из удалённой ветви и сливает их со своей текущей ветвью. 
$ touch README.md
Создает файл README.md в текущей папке.
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        README.md

nothing added to commit but untracked files present (use "git add" to track)
Команда проверяет состояние текущего репозитория и сообщает, есть ли изменения или нет.
$ git add README.md
Команда вносит изменения в файл README.md.
$ git commit -m"added README.md"
[master (root-commit) f7740f7] added README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
 Команда сохраняет изменения. Опция -m означает, что можно добавить комментарий к коммиту.
$ git push origin master
Username for 'https://github.com': AlexDeveloper24
Password for 'https://AlexDeveloper24@github.com': 
Counting objects: 3, done.
Writing objects: 100% (3/3), 228 bytes | 228.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/AlexDeveloper24/lab03.git
 * [new branch]      master -> master
 Команда отправляет наши изменения в удаленный репозиторий.
```

Добавить на сервисе **GitHub** в репозитории **lab03** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
.idea/
```

```ShellSession
$ git pull origin master
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/AlexDeveloper24/lab03
 * branch            master     -> FETCH_HEAD
   f7740f7..3dcad21  master     -> origin/master
Updating f7740f7..3dcad21
Fast-forward
 .gitignore | 4 ++++
 1 file changed, 4 insertions(+)
 create mode 100644 .gitignore
Команда автоматически извлекает и затем сливает данные из удалённой ветки в нашу текущую ветку. 
$ git log
commit 3dcad21e59e3f50104dcd004b1cd1b9df56ccbc8 (HEAD -> master, origin/master)
Author: AlexDeveloper24 <36934474+AlexDeveloper24@users.noreply.github.com>
Date:   Sat Mar 17 23:52:32 2018 +0300

    Create .gitignore

commit f7740f7ddbe9f1970ebbc75bc4aa0537e0166574
Author: AlexDeveloper24 <alexchubukov12345@gmail.com>
Date:   Sat Mar 17 19:48:32 2018 +0000

    added README.md
Команда выводит историю коммитов.
```

```ShellSession
$ mkdir sources
Создали папку sources.
$ mkdir include
Создали папку include.
$ mkdir examples
Создали папку examples.
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out) {
  out << text;
}

void print(const std::string& text, std::ofstream& out) {
  out << text;
}
EOF
Команда cat > выводит содержимое между EOF в файл sources/print.cpp.
```

```ShellSession
$ cat > include/print.hpp <<EOF
#include <string>
#include <fstream>
#include <iostream>

void print(const std::string& text, std::ostream& out = std::cout);
void print(const std::string& text, std::ofstream& out);
EOF
Команда cat > выводит содержимое между EOF в файл include/print.hpp.
```

```ShellSession
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv) {
  print("hello");
}
EOF
Команда cat > выводит содержимое между EOF в файл examples/example1.cpp.
```

```ShellSession
$ cat > examples/example2.cpp <<EOF
#include <fstream>
#include <print.hpp>

int main(int argc, char** argv) {
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
Команда cat > выводит содержимое между EOF в файл examples/example2.cpp.
```

```ShellSession
$ edit README.md
Изменям файл README.md, создаем отчет.
```

```ShellSession
$ git status
$ git add .
$ git commit -m"added sources"
$ git push origin master
```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=03
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2017 Братья Вершинины
```

