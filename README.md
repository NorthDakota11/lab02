# lab02
lab02
Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере Git.

$ open https://git-scm.com
Tasks

Создать публичный репозиторий с названием lab02 и с лиценцией MIT
Сгенирировать токен для доступа к сервису GitHub с правами repo
Ознакомиться со ссылками учебного материала
Выполнить инструкцию учебного материала
Составить отчет и отправить ссылку личным сообщением в Slack
Tutorial

$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=<nano|vi|vim|subl>
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
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
Добавить на сервисе GitHub в репозитории lab02 файл .gitignore со следующем содержимом:

*build*/

*install*/

*.swp

.idea/
$ git pull origin master
$ git log
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
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>
#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
$ edit README.md
$ git status
$ git add .
$ git commit -m"added sources"
$ git push origin master
Report

$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
Homework
Part I
Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
Создан репозиторий lab02.

Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
Первый коммит создан.

Создайте файл hello_world.cpp в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу Hello world на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку using namespace std;.
$ nano hello_world.cpp
Добавьте этот файл в локальную копию репозитория.
$ git add hello_world.cpp
Закоммитьте изменения с осмысленным сообщением.
$ git commit -m "Был добавлен файл hello_world.cpp и реализована программа вывода"
Вывод:

[master d08687d] Был добавлен файл hello_world.cpp и реализована программа вывода
 1 file changed, 7 insertions(+)
 create mode 100644 hello_world.cpp
Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение Hello world from @name, где @name имя пользователя.
$ nano hello_world.cpp
Теперь программа выглядит так:

#include <iostream>
#include <string>
using namespace std;

int main() {
    string name;
    cout<<"Введите свое имя: ";
    cin>>name;
    cout << "Hello world from " << name<< endl;
    return 0;
}
Закоммитьте новую версию программы. Почему не надо добавлять файл повторно git add?
$ git commit -am "Изменен файл hello_world.cpp"
Вывод:

[master 6dda9fd] Изменен файл hello_world.cpp
 1 file changed, 5 insertions(+), 1 deletion(-)
Git уже отслеживает все файлы и добавляет их автоматически.

Запуште изменения в удалёный репозиторий.
$ git push origin master
Вывод:

Username for 'https://github.com': NorthDakota11
Password for 'https://pwc972@github.com': 
Перечисление объектов: 7, готово.
Подсчет объектов: 100% (7/7), готово.
При сжатии изменений используется до 4 потоков
Сжатие объектов: 100% (6/6), готово.
Запись объектов: 100% (6/6), 867 байтов | 867.00 КиБ/с, готово.
Всего 6 (изменений 1), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/NorthDakota11-stack/lab02.git
   3693016..6dda9fd  master -> master
Проверьте, что история коммитов доступна в удалёный репозитории.
$ git log
Вывод:

commit 6dda9fd049f7cf0bf163424f5f3440a7903a8b5b (HEAD -> master, origin/master)
Author: pwc972 <@gmail.com>
Date:   Tue Mar 3 14:14:54 2026 +0300

    Изменен файл hello_world.cpp

commit d08687d820138109bc70520a38a2238bcac93611
Author: pwc972 <@gmail.com>
Date:   Tue Mar 3 14:05:52 2026 +0300

    Был добавлен файл hello_world.cpp и реализована программа вывода

commit 3693016e4efa5be29728a7b81b8fac6a4d1222f8
Author: misakontileev-stack <pwc972@gmail.com>
Date:   Tue Mar 3 13:50:39 2026 +0300

    Add .gitignore

commit ef4a6df66b341a52d96f633102e14ab4406606c6
Author: misakontileev-stack <pwc972@gmail.com>
Date:   Tue Mar 3 12:51:32 2026 +0300

    Initial commit
Part II
Note: Работать продолжайте с теми же репоззиториями, что и в первой части задания.

В локальной копии репозитория создайте локальную ветку patch1.
$ git checkout -b patch1
Вывод:

Переключились на новую ветку «patch1»
Внесите изменения в ветке patch1 по исправлению кода и избавления от using namespace std;.
$ nano hello_world.cpp
Теперь код выглядит так:

#include <iostream>
#include <string>

int main() {
    std::string name;
    std::cout << "Введите свое имя: ";
    std::cin >> name;
    std::cout << "Hello world from " << name << std:: endl;
    return 0;
}
commit, push локальную ветку в удалённый репозиторий.
$ git commit -am "Удалена строчка кода: using namespace std, и к каждой строчке добавлено: std::"
Вывод:

[patch1 81a86ff] Удалена строчка кода: using namespace std, и к каждой строчке добавлено: std::
 1 file changed, 4 insertions(+), 5 deletions(-)
$ git push origin patch1
Вывод:

Username for 'https://github.com': NorthDakota11
Password for 'https://pwc972@github.com': 
Перечисление объектов: 5, готово.
Подсчет объектов: 100% (5/5), готово.
При сжатии изменений используется до 4 потоков
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (3/3), 478 байтов | 478.00 КиБ/с, готово.
Всего 3 (изменений 1), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/NorthDakota11-stack/lab02/pull/new/patch1
remote: 
To https://github.com/misakontileev-stack/lab02.git
 * [new branch]      patch1 -> patch1
Проверьте, что ветка patch1 доступна в удалёный репозитории.
На Github ветка patch1 присутствует.

Создайте pull-request patch1 -> master.
Pull-request создан.

В локальной копии в ветке patch1 добавьте в исходный код комментарии.
$ nano hello_world.cpp
Теперь код такой:

#include <iostream>
#include <string>

//Основная функция
int main() {
    std::string name; //Создана строковая переменная
    std::cout << "Введите свое имя: "; //Вывод запроса
    std::cin >> name; //Ввод имени
    std::cout << "Hello world from " << name << std:: endl; //Вывод конечного результата
    return 0;
}
commit, push.
$ git commit -am "Добавлены комментарии."
Вывод:

[patch1 27030e3] Добавлены комментарии.
 2 files changed, 323 insertions(+), 5 deletions(-)
$ git push origin patch1
Вывод:

Username for 'https://github.com': NorthDakota11
Password for 'https://pwc972@github.com': 
Перечисление объектов: 7, готово.
Подсчет объектов: 100% (7/7), готово.
При сжатии изменений используется до 4 потоков
Сжатие объектов: 100% (4/4), готово.
Запись объектов: 100% (4/4), 4.07 КиБ | 4.07 МиБ/с, готово.
Всего 4 (изменений 0), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
To https://github.com/NorthDakota11-stack/lab02.git
   81a86ff..27030e3  patch1 -> patch1
Проверьте, что новые изменения есть в созданном на шаге 5 pull-request
Все изменения есть.

В удалённый репозитории выполните слияние PR patch1 -> master и удалите ветку patch1 в удаленном репозитории.
Слияние выполнено.

$ git checkout master
Вывод:

Переключились на ветку «master»
Эта ветка соответствует «origin/master».
Локально выполните pull.
$ git pull origin master
Вывод:

remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Распаковка объектов: 100% (1/1), 991 байт | 991.00 КиБ/с, готово.
Из https://github.com/NorthDakota11-stack/lab02
 * branch            master     -> FETCH_HEAD
   6dda9fd..e543b53  master     -> origin/master
Обновление 6dda9fd..e543b53
Fast-forward
 README.md       | 319 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-
 hello_world.cpp |  10 ++--
 2 files changed, 323 insertions(+), 6 deletions(-)
С помощью команды git log просмотрите историю в локальной версии ветки master.
$ git log
Вывод:

commit e543b536731c2c62a86f0ed7c11e19725199556a (HEAD -> master, origin/master)
Merge: 6dda9fd 27030e3
Author: NorthDakota11-stack <pwc972@gmail.com>
Date:   Tue Mar 3 14:49:39 2026 +0300

    Merge pull request #1 from misakontileev-stack/patch1
    
    Удалена строчка кода: using namespace std, и к каждой строчке добавле…

commit 27030e31c1deaf4628f6e42a7c8fe8e8e2339430 (origin/patch1)
Author: pwc972 <@gmail.com>
Date:   Tue Mar 3 14:44:45 2026 +0300

    Добавлены комментарии.

commit 81a86ff38898587e130d1a5264ed35eaa820dce4
Author: pwc972 <@gmail.com>
Date:   Tue Mar 3 14:30:02 2026 +0300

    Удалена строчка кода: using namespace std, и к каждой строчке добавлено: std::

commit 6dda9fd049f7cf0bf163424f5f3440a7903a8b5b
Author: pwc972 <@gmail.com>
Date:   Tue Mar 3 14:14:54 2026 +0300

    Изменен файл hello_world.cpp

commit d08687d820138109bc70520a38a2238bcac93611
Author: pwc972 <@gmail.com>
Date:   Tue Mar 3 14:05:52 2026 +0300

    Был добавлен файл hello_world.cpp и реализована программа вывода
Удалите локальную ветку patch1.
$ git branch -d patch1
Вывод:

Ветка patch1 удалена (была 27030e3).
Part III
Note: Работать продолжайте с теми же репоззиториями, что и в первой части задания.

Создайте новую локальную ветку patch2.
$ git checkout -b patch2
Вывод:

Переключились на новую ветку «patch2»
Измените code style с помощью утилиты clang-format. Например, используя опцию -style=Mozilla.
$ clang-format -i -style=Mozilla hello_world.cpp
commit, push, создайте pull-request patch2 -> master.
$ git commit -am "Изменен стиль с помощью опции -style=Mozilla"
Вывод:

[patch2 51f30a1] Изменен стиль с помощью опции -style=Mozilla
 1 file changed, 10 insertions(+), 7 deletions(-)
$ git push origin patch2
Вывод:

Username for 'https://github.com': misakontileev
Password for 'https://misakontileev@github.com': 
Перечисление объектов: 5, готово.
Подсчет объектов: 100% (5/5), готово.
При сжатии изменений используется до 4 потоков
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (3/3), 435 байтов | 435.00 КиБ/с, готово.
Всего 3 (изменений 2), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
remote: 
remote: Create a pull request for 'patch2' on GitHub by visiting:
remote:      https://github.com/misakontileev-stack/lab02/pull/new/patch2
remote: 
To https://github.com/misakontileev-stack/lab02.git
 * [new branch]      patch2 -> patch2
В ветке master в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
Изменены комментарии.

Убедитесь, что в pull-request появились конфликтны.
Конфикты появились, теперь нельзя произвести слияние.

Для этого локально выполните pull + rebase (точную последовательность команд, следует узнать самостоятельно). Исправьте конфликты.
$ git pull --rebase origin master
Вывод:

Из https://github.com/NorthDakota11-stack/lab02
 * branch            master_test -> FETCH_HEAD
Автослияние hello_world.cpp
КОНФЛИКТ (содержимое): Конфликт слияния в hello_world.cpp
error: не удалось применить коммит 8627f29... Изменен стиль с помощью clang-format
подсказка: Resolve all conflicts manually, mark them as resolved with
подсказка: "git add/rm <conflicted_files>", then run "git rebase --continue".
подсказка: You can instead skip this commit: run "git rebase --skip".
подсказка: To abort and get back to the state before "git rebase", run "git rebase --abort".
Не удалось применить коммит 8627f29... Изменен стиль с помощью clang-format
Сделайте force push в ветку patch2
Отредактировал файл обратно.

$ git add hello_world.cpp

$ git rebase --continue
Вывод:

[отделённый HEAD e8ca849] Изменен стиль с помощью clang-format
 1 file changed, 1 insertion(+), 1 deletion(-)
Успешно перемещён и обновлён refs/heads/patch2.
$ git push -f origin patch2
Вывод:

Username for 'https://github.com': NorthDakota11
Password for 'https:/pwc972@github.com': 
Перечисление объектов: 5, готово.
Подсчет объектов: 100% (5/5), готово.
При сжатии изменений используется до 4 потоков
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (3/3), 359 байтов | 359.00 КиБ/с, готово.
Всего 3 (изменений 2), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/misakontileev-stack/lab02.git
 + 8627f29...e8ca849 patch2 -> patch2 (forced update)
Убедитеcь, что в pull-request пропали конфликтны.
Все конфикты устранены удаленно через GinHub. Был возвращен прежний вид файла hello_world.cpp.

Вмержите pull-request patch2 -> master.
Слияние сделано.
