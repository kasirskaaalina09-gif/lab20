## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [ ] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [ ] 3. Ознакомиться со ссылками учебного материала
- [ ] 4. Выполнить инструкцию учебного материала
- [ ] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=<nano|vi|vim|subl>
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
```

```sh
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
```

```sh
$ mkdir projects/lab02 && cd projects/lab02
$ git init
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master
$ touch README.md
$ git status
$ git add README.md
$ git commit -m"added README.md"
$ git push origin master
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
$ git pull origin master
$ git log
```

```sh
$ mkdir sources
$ mkdir include
$ mkdir examples
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
```

```sh
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```sh
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```sh
$ cat > examples/example2.cpp <<EOF
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
$ edit README.md
```

```sh
$ git status
$ git add .
$ git commit -m"added sources"
$ git push origin master
```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).

Создан репозиторий lab20 на github.com

2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.

Выполнен первый коммит на файл .gitignore

3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.

Команды:

```bash
$ touch hello_world.cpp
$ nano hello_world.cpp
```

4. Добавьте этот файл в локальную копию репозитория.

Команда:

```bash 
$ git add hello_world.cpp
```

5. Закоммитьте изменения с *осмысленным* сообщением.

Команда:

```bash
$ git commit -m "Added hello_world.cpp"
```
Вывод:

```bash
[main d7ea42b] Added Hello_world.cpp
 1 file changed, 8 insertions(+)
 create mode 100644 hello_world.cpp
```

6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.

Команда:

```bash
$ nano hello_world.cpp
```

Теперь файл выглядит так:

```bash
#include <iostream>
#include <string>

using namespace std;

int main() {
    string name;
    cout<<"Enter your name: ";
    cin>>name;
    cout<<"Hello world from "<<name<<endl;
    return 0;
}
```

7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?

Команда:

```bash
$ git commit -am "Added changed hello_world.cpp"
```
Вывод:

```bash
[main 0a50119] Added changed hello_world.cpp
 1 file changed, 5 insertions(+), 1 deletion(-)
```
Файл не нужно добавлять повторно так как git его уже отслеживает

8. Запуште изменения в удалёный репозиторий.

Команда:

```bash 
$ git push origin main
```

9. Проверьте, что история коммитов доступна в удалёный репозитории.

Команда:

```bash
$ git log
```

Вывод:

```bash
commit 0a50119c26ab00525139c73104bb43b2ba145a90 (HEAD -> main, origin/main)
Author: kasirskaaalina09-gif <kasirskaaalina09@gmail.com>
Date:   Mon Apr 27 11:16:42 2026 +0000

    Added changed hello_world.cpp

commit d7ea42bccfacfc26891f3f51d4d93500df93a4e0
Author: kasirskaaalina09-gif <kasirskaaalina09@gmail.com>
Date:   Mon Apr 27 11:12:26 2026 +0000

    Added Hello_world.cpp

commit 6f1145de8902b2967e4430a7916d55c84dd3ef62
Author: kasirskaaalina09-gif <kasirskaaalina09@gmail.com>
Date:   Mon Apr 27 10:54:40 2026 +0000

    added .gitignore
```

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.

Команда:

```bash
$ git checkout -b patch1
```
Вывод:

```bash
Switched to a new branch 'patch1'
```

2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.

Команды:

```bash
$ nano hello_world.cpp
```
Измененный файл(убран using namespace std;):

```bash
#include <iostream>
#include <string>

int main() {
    std::string name;
    std::cout<<"Enter your name: ";
    std::cin>>name;
    std::cout<<"Hello world from "<<name<<std::endl;
    return 0;
}
```

3. **commit**, **push** локальную ветку в удалённый репозиторий.

Команды:

```bash
$ git commit -am "using namespace std was deleted from hello_world.cpp"
```
```bash
$ git push origin patch1
```

Вывод(для git commit):

```bash
[patch1 8bf45f7] using namespace std was deleted from hello_world.cpp
 1 file changed, 4 insertions(+), 6 deletions(-)
```

Вывод(для git push):

```bash
Username for 'https://github.com': kasirskaaalina09-gif
Password for 'https://kasirskaaalina09-gif@github.com': 
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 440 bytes | 440.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/kasirskaaalina09-gif/lab20/pull/new/patch1
remote: 
To https://github.com/kasirskaaalina09-gif/lab20.git
 * [new branch]      patch1 -> patch1
```

4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.

В удаленном репозитории ветка patch1 доступна

5. Создайте pull-request `patch1 -> master`.

Создан pull-request

6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.

Команда:

```bash
$ nano gello_world.cpp
```
Файл с добавленным комментарием теперь выглядит так:

```bash
#include <iostream>
#include <string>

//main func
int main() {
    std::string name;
    std::cout<<"Enter your name: ";
    std::cin>>name;
    std::cout<<"Hello world from "<<name<<std::endl;
    return 0;
}
```

7. **commit**, **push**.

Команды:

```bash
git commit -am "added comment to hello_world.cpp"
```

```bash
git push origin patch1
```

Вывод(для git commit):

```bash
[patch1 9f8fe09] added comment to hello_world.cpp
 1 file changed, 1 insertion(+)
```

Вывод(для git push):

```bash
Username for 'https://github.com': kasirskaaalina09-gif
Password for 'https://kasirskaaalina09-gif@github.com': 
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 343 bytes | 343.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/kasirskaaalina09-gif/lab20.git
   8bf45f7..9f8fe09  patch1 -> patch1
```

8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request

Новые изменения появились

9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.

Слияние выполнено

```bash
$ git checkout main
```
Вывод:

```bash
Switched to branch 'main'
```

10. Локально выполните **pull**.

Команда:

```bash
$ git pull origin main
```

Вывод:

```bash
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (1/1), 916 bytes | 916.00 KiB/s, done.
From https://github.com/kasirskaaalina09-gif/lab20
 * branch            main       -> FETCH_HEAD
   0a50119..b5e97a1  main       -> origin/main
Updating 9f8fe09..b5e97a1
Fast-forward
```

11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.

Команда:

```bash
$ git log
```

Вывод:

```bash
commit b5e97a1568d06494c3f6de58d2167581b2cb2d70 (HEAD -> patch1, origin/main)
Merge: 0a50119 9f8fe09
Author: kasirskaaalina09-gif <kasirskaaalina09@gmail.com>
Date:   Mon Apr 27 11:42:40 2026 +0000

    Merge pull request #1 from kasirskaaalina09-gif/patch1
    
    using namespace std was deleted from hello_world.cpp

commit 9f8fe0932bd952790d86e186d7f3dcdc9613614f (origin/patch1)
Author: kasirskaaalina09-gif <kasirskaaalina09@gmail.com>
Date:   Mon Apr 27 11:40:08 2026 +0000

    added comment to hello_world.cpp

commit 8bf45f7eee8b12b690c697a2f2ab29b043370428
Author: kasirskaaalina09-gif <kasirskaaalina09@gmail.com>
Date:   Mon Apr 27 11:25:16 2026 +0000

    using namespace std was deleted from hello_world.cpp

commit 0a50119c26ab00525139c73104bb43b2ba145a90 (main)
Author: kasirskaaalina09-gif <kasirskaaalina09@gmail.com>
Date:   Mon Apr 27 11:16:42 2026 +0000

    Added changed hello_world.cpp

commit d7ea42bccfacfc26891f3f51d4d93500df93a4e0
Author: kasirskaaalina09-gif <kasirskaaalina09@gmail.com>
Date:   Mon Apr 27 11:12:26 2026 +0000

    Added Hello_world.cpp

commit 6f1145de8902b2967e4430a7916d55c84dd3ef62
Author: kasirskaaalina09-gif <kasirskaaalina09@gmail.com>
Date:   Mon Apr 27 10:54:40 2026 +0000

    added .gitignore
```

12. Удалите локальную ветку `patch1`.

Команда:

```bash
$ git branch -d patch1
```

Вывод:

```bash
Deleted branch patch1 (was b5e97a1).
```

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.

Команда:

```bash
$ git checkout -b patch2
```

Вывод:

```bash
Switched to a new branch 'patch2'
```

2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.

Команда:

```bash
$ clang-format -i -style=Mozilla hello_world.cpp
```


3. **commit**, **push**, создайте pull-request `patch2 -> master`.

Команды:

```bash
$ git commit -am "Style was changed by option -style=Mozilla"
```

```bash
$ git push origin patch2
```

Вывод(для git commit):

```bash
[patch2 216b810] Style was changed by option -style=Mozilla
 1 file changed, 8 insertions(+), 6 deletions(-)
```

Вывод(для git push):

```bash
Username for 'https://github.com': kasirskaaalina09-gif
Password for 'https://kasirskaaalina09-gif@github.com': 
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 442 bytes | 442.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'patch2' on GitHub by visiting:
remote:      https://github.com/kasirskaaalina09-gif/lab20/pull/new/patch2
remote: 
To https://github.com/kasirskaaalina09-gif/lab20.git
 * [new branch]      patch2 -> patch2
```

4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.

Комментарий изменен

5. Убедитесь, что в pull-request появились *конфликтны*.

Конфликты появились и слияние теперь провести нельзя

6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.

Команды:

```bash
$ git pull --rebase origin main
```

Вывод:

```bash
git pull --rebase origin main
From https://github.com/kasirskaaalina09-gif/lab20
 * branch            main       -> FETCH_HEAD
Auto-merging hello_world.cpp
CONFLICT (content): Merge conflict in hello_world.cpp
error: could not apply 216b810... Style was changed by option -style=Mozilla
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply 216b810... Style was changed by option -style=Mozilla
```

7. Сделайте *force push* в ветку `patch2`

Была выбрана итоговая версия файла hello_world.cpp

Команды:

```bash
$ git add hello_worl.cpp
```

```bash
$ git rebase --continue
```

Вывод:

```bash
[detached HEAD 7d8f34e] Style was changed by option -style=Mozilla
 1 file changed, 8 insertions(+), 7 deletions(-)
```

```bash 
$ git push -f origin patch2
```

Вывод:

```bash
Username for 'https://github.com': kasirskaaalina09-gif
Password for 'https://kasirskaaalina09-gif@github.com': 
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 563 bytes | 563.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/kasirskaaalina09-gif/lab20.git
 + 216b810...7d8f34e patch2 -> patch2 (forced update)
```

8. Убедитель, что в pull-request пропали конфликтны.

Все конфликты были устранены, была выбрана итоговая версия файла hello_world.cpp, теперь можно провести слияние
 
9. Вмержите pull-request `patch2 -> master`.

Слияние прошло успешно

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2021 The ISC Authors
```
