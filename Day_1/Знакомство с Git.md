# Знакомство с Git

# Основные понятия

Git - это распределенная система управления версиями (VCS), используемая для отслеживания изменений в исходном коде и координации работы нескольких разработчиков над проектом.  \n Git облегчает совместную работу разработчиков, отслеживание изменений в коде, управление версиями и решение конфликтов. Он широко используется в индустрии разработки программного обеспечения и является ключевым инструментом для многих проектов.

При этом не надо путать Git и GitHub. Последний является хранилищем репозиториев и просто социальной сетью для разработчиков. Некоторые примеры будут показаны именно в GitHub, так как с ним приходится работать чаще всего

## Основные концепции Git


1. **Репозиторий (Repository):** Git хранит данные в структуре, называемой репозиторием. Репозиторий содержит исходный код, историю изменений, ветки и другую информацию о проекте. \n  ![](/api/attachments.redirect?id=31a623f8-81fc-48be-a11a-38c4bfb80344 "aspect=1")
2. **Коммит (Commit):** Коммит представляет собой сохраненное состояние репозитория в определенный момент времени. Каждый коммит содержит изменения в файлах и метаданные, такие как автор и сообщение о коммите. ![](/api/attachments.redirect?id=6bf2f9e1-2e92-4312-b992-eecbeec279d3 "aspect=1")
3. **Ветвление (Branching):** Git позволяет создавать ветки, что дает возможность разработчикам работать над различными фрагментами кода параллельно. Ветки могут объединяться, чтобы интегрировать изменения.

   ```bash
   test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$ git branch
   * main
   test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$
   ```

   С помощью команды git branch можно посмотреть, какие ветки доступны в репозитории, а “*” указывыет в какой ветке мы находимся

   ```bash
   test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$ git branch test
   test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$ git checkout test
   Switched to branch 'test'
   test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$ git branch
     main
   * test
   test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$
   ```

   Для создания новой ветки используется команда git branch <branch_name>

   Для того, чтобы переключиться на любую из доступных веток git checkout <branch_name> \n Удалить ветку можно с помощью git branch -d <branch_name>

   \
4. **Слияние (Merging):** Слияние в Git позволяет объединить изменения из одной ветви в другую. Это позволяет интегрировать новые функции или исправления ошибок в основной код. \n 
5. **Отслеживание изменений (Tracking Changes):** Git отслеживает изменения в файлах и эффективно передает только те изменения, которые были внесены, что делает передачу данных более эффективной.

# Установка Git и создание репозитория

**Прежде чем начать работать с Git, у*станавливаем его себе на устройств, следуя [инструкции в статье](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)***


Для того, чтобы создать репозиторий в нужном нам каталоге, пользуемся командой git init

```bash
test@DESKTOP:~/Desktop/test$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>
Initialized empty Git repository in ~/Desktop/test/.git/
test@DESKTOP:~/Desktop/test$
```

Здесь мы инициализировали пустой репозиторий в каталоге test/ \n Теперь когда мы будем создавать файлы в этом каталоге, они будут храниться в репозитории test по умолчанию в ветке master или main. 

 \n Создадим тестовый файл и посмотрим состояние репозитория. Для этого используем команды touch <file_name> , а затем git status

```bash
test@DESKTOP:~/Desktop/test$ touch test.c
test@DESKTOP:~/Desktop/test$ git status
On branch master

No commits yet

Untracked files:                                      
  (use "git add <file>..." to include in what will be committed)
        test.c

nothing added to commit but untracked files present (use "git add" to track)
test@DESKTOP:~/Desktop/test$       
```

Рассмотрим вывод git status подробнее: \n On branch master - указывает в какой ветке мы сейчас находимся \n No commits yet - говорит о том, что никаких коммитов пока что нет \n Untracked files: - файлы, которые лежат в каталоге, но изменения в них пока не отслеживаются


Для того, чтобы Git смог отслеживать изменения в ваших файлах существует команда  \n git add <file_name> \n Используем ее, чтобы добавить наш файл и проверяем через git status

```bash
test@DESKTOP:~/Desktop/test$ git add test.c
test@DESKTOP:~/Desktop/test$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   test.c

test@DESKTOP:~/Desktop/test$
```

Видим, что пропал раздел Untracked files:, но появился новый Changes to be commited, который говорит нам, какие файлы подлежат коммиту

***Чтобы добавить все файлы разом используйте “*” или “.“ вместо имени файла*** \n ***Пример: git add ****

Создадим свой первый коммит при помощи команды git commit -m ‘first_commit‘ и получаем вот такой вывод

```bash
test@DESKTOP:~/Desktop/test$ git commit -m 'first_commit'
Author identity unknown

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: empty ident name (for <test@DESKTOP.>) not allowed
test@DESKTOP:~/Desktop/test$
```

Который прямо говорит нам, что пользователь, совершающий коммит, не идентифицирован


Исправляем ситуацию, запуская 2 команды git config и смотрим git status

```bash
test@DESKTOP:~/Desktop/test$ git config --global user.email "example@gmail.com"
test@DESKTOP:~/Desktop/test$ git config --global user.name "Test_name"
test@DESKTOP:~/Desktop/test$ git commit -m 'first_commit'
[master (root-commit) 4100966] first_commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test.c
test@DESKTOP:~/Desktop/test$ git status
On branch master
nothing to commit, working tree clean
test@DESKTOP:~/Desktop/test$
```

В команде git commit -m ““ в двойных кавычках пишем название коммита, это важно для документирования вносимых изменений


Как посмотреть все коммиты в нашей ветке? \n Есть несколько способов, но мы воспользуемся командой git log

```bash
test@DESKTOP:~/Desktop/test$ git log
commit 410096609f3eefde9dce56bf0cf2c79229eb583c (HEAD -> master)
Author: Test_name <example@gmail.com>
Date:   Sat Dec 23 13:39:35 2023 +0400

    first_commit
test@DESKTOP:~/Desktop/test$
```

В выводе видим автора, дату и имя коммита

Теперь мы знаем, как работать с репозиторием локально, остается узнать, как работать с удаленным

# Работа с удаленным репозиторием

Для примера будем работать с GitHub

***Чтоб двигаться дальше необходимо самостоятельно зарегистрироваться на [github.com](http://github.com)и создать репозиторий.  Надеюсь, с этим проблем не возникнет 🙃***


На картинке показано, как происходит клонирование репозитория на локальное устройство и отправка изменений на сервер ![](/api/attachments.redirect?id=080773f1-e33f-4612-ae65-f18cd0eb23c5 "aspect=1")

## Клонирование репозитория

Для того, чтобы склонировать нужный нам репозиторий для начал нужно достать на него ссылку \n  ![](/api/attachments.redirect?id=2d4f809b-573a-4a06-8d97-044ba406b617 "aspect=1")

Затем идем в терминал и вводим следующую команду

```bash
test@DESKTOP:~/Desktop$ git clone https://github.com/Stanislavmg/Piscine-C-Ecole-42.git
Cloning into 'Piscine-C-Ecole-42'...
remote: Enumerating objects: 415, done.
remote: Counting objects: 100% (415/415), done.
remote: Compressing objects: 100% (120/120), done.
remote: Total 415 (delta 185), reused 381 (delta 157), pack-reused 0
Receiving objects: 100% (415/415), 4.46 MiB | 2.37 MiB/s, done.
Resolving deltas: 100% (185/185), done.
Updating files: 100% (128/128), done.
test@DESKTOP:~/Desktop$ cd Piscine-C-Ecole-42/
test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$ ls
README.md  c_00  c_01  c_02  c_03  c_04  c_05  c_06  c_07  c_08  c_09  rush_00  rush_01  rush_02  shell_00  shell_01
test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$
```

и получаем точную копию репозитория у на компьютере со всеми данными в нем

## Внесение изменений в удаленный репозиторий

Итак, репозиторий склонировали, работаем в нем локально, пишем код, создаем коммит. Как теперь отправить все изменения в удаленный репозиторий? \n Все это можно сделать с помощью одной команды, но для начала нужно пройти авторизацию на удаленном сервере, в данном случае на GitHub

Существует 2 способа это сделать:  \n - с помощью токена \n - по протоколу SSH


Авторизация по протоколу SSH происходит в 2 этапа:


1. Генерация ключевой пары
2. Добавление публичного ключа в личный кабинет GitHub

   *Подробнее о том, как работает SSH соединение можно посмотреть в разделе “/Резюме/Используемые материалы“*

```bash
test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/test/.ssh/id_rsa):
Created directory '/home/stanislav/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/test/.ssh/id_rsa
Your public key has been saved in /home/test/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:o5eAZ/aGaUrWdLcHhyOdVjOPLNuVFPnGn+6bzyyBNOU test@DESKTOP
The key's randomart image is:
+---[RSA 3072]----+
|            ..   |
|           ....  |
|          . +=   |
|     .   o BooE  |
|    . * S @.=+ ..|
|     * B X *. ...|
|    o * * o . .. |
|   o o o   .  .+.|
|    .         .=*|
+----[SHA256]-----+
test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$
```

Теперь нам нужно скопировать содержимое файла /home/test/.ssh/id_rsa.pub в личный кабинет GItHub

Заходим в настройки профиля и в разделе SSH and GPG keys добавляем наш ключик

 ![](/api/attachments.redirect?id=bbc24f72-0034-43b2-bb10-257c97984358 "aspect=1")

Последнее что от нас требуется перед тем, как сделать push всех изменений - установить доступ к удаленному репозиторию по протоколу SSH \n Делаем это с помощью команды git remote set-url origin <ssh_url>

ssh_url можно получить там же, где мы копировали HTTPS url

```bash
test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$ git remote set-url origin git@github.com:Stanislavmg/Piscine-C-Ecole-42.git
test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$ git push -u origin main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 303 bytes | 14.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:Stanislavmg/Piscine-C-Ecole-42.git
   0fd59b2..c7a63b0  main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
test@DESKTOP:~/Desktop/Piscine-C-Ecole-42$
```

После этого пушим наши изменения командой git push -u origin main

# Резюме

Сегодня я постарался познакомить тебя с Gitом, надеюсь, это знакомство было для тебя максимально безболезненным. Помни, что это всего лишь первая встреча и для того, чтобы по-настоящему научиться пользоваться эти инструментом, тебе понадобиться потратить еще очень много времени на самостоятельное обучение

## Основные команды, которые нужно знать, работая с Git:

git init \n git status

git add

git commit \n git log

git config

git branch

git checkout \n git clone

git set-url

git push

ssh-keygen

## Используемые материалы

[Первоначальная настройка Git](https://git-scm.com/book/ru/v2/%D0%92%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5-%D0%9F%D0%B5%D1%80%D0%B2%D0%BE%D0%BD%D0%B0%D1%87%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-Git)

[Создание Git-репозитория](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%A1%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-Git-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F)

[Просмотр истории коммитов](https://git-scm.com/book/ru/v2/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%9F%D1%80%D0%BE%D1%81%D0%BC%D0%BE%D1%82%D1%80-%D0%B8%D1%81%D1%82%D0%BE%D1%80%D0%B8%D0%B8-%D0%BA%D0%BE%D0%BC%D0%BC%D0%B8%D1%82%D0%BE%D0%B2)

[Основы ветвления и слияния](https://git-scm.com/book/ru/v2/%D0%92%D0%B5%D1%82%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B2-Git-%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-%D0%B2%D0%B5%D1%82%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B8-%D1%81%D0%BB%D0%B8%D1%8F%D0%BD%D0%B8%D1%8F)

[Генерация открытого SSH ключа](https://git-scm.com/book/ru/v2/Git-%D0%BD%D0%B0-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80%D0%B5-%D0%93%D0%B5%D0%BD%D0%B5%D1%80%D0%B0%D1%86%D0%B8%D1%8F-%D0%BE%D1%82%D0%BA%D1%80%D1%8B%D1%82%D0%BE%D0%B3%D0%BE-SSH-%D0%BA%D0%BB%D1%8E%D1%87%D0%B0)

[Добавление нового ключа SSH в учетную запись GitHub](https://docs.github.com/ru/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

Как работает SSH

# Практическое задание


1. Зарегистрироваться на [github.com](http://github.com)
2. Создать репозиторий “FB_learning“ 
3. Склонировать репозиторий на свое устройство
4. В файле README.md добавить публичный SSH ключ
5. Создать каталог “1_day”
6. Запушить все изменения в удаленный репозиторий

   \


