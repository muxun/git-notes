# git notes

# Про git

git -  это распределенная система контроля версий 

git в своих коммитах хранит полное состояние ветки. в отличии от svn, которая хранит diff 

система хранения git репозитория состоит из  4 объектов :

- blob
- tree
- commit
- tag

**blob -** базовая единица хранения данных.Хранит снепшот содержимого файла. В качестве имени объекта берется sha1 хэш содержимого файла и заголовка

**tree -** деревья содержат информацию о блобах, а также других поддеревьях.

# Git Workflow

![](gwf-31ba7b10-c767-4ca8-8556-16d6c79caf59.png)

# Установка и настройка

установка на ubuntu like системах

    $ sudo apt install git   

конфиг для взаимодействия с github

    $ git config --global user.name "username"
    $ git config --global user.email "username.user@example.com"

оценить конфиг

    $ git config --list

# $shell надстройки

настройка bash на отображение ветки и статуса индекса

    cd ~
    git clone https://github.com/magicmonty/bash-git-prompt.git .bash-git-prompt --depth=1

затем, в конец .bashrc добавить строки 

    GIT_PROMPT_ONLY_IN_REPO=1
    source ~/.bash-git-prompt/gitprompt.sh

для применения изменений перезапустить bash

    exec bash

# Работа с локальным репозиторием

создание репозитория  производится командой init в папке назначения

    git init

теперь git отслеживает все изменения файлов  папке. чтобы не отслеживать мусорные файлу, нужно их занести в .gitignore

    echo "*.trash" >> .gitignore

поработали,изменили файлики, заносим в индекс измененные  файлы

    git add *.changed_files

решили сделать коммит

    git commit -m "Change some files"

флаг -m и сообщение после - обязательные атрибуты коммита.

поработали еще, заносим измененные файлики в индекс (git add), ибо непроиндексированные изменения в коммит не уйдут.

команды для просмотра информации о состоянии репозитория

    git diff

    git log

    git status

# Аутентификация на github

Для аутентификации на github по ssh ключам  генерим ключи с аккаунтом github

    $ ssh-keygen -t rsa -b 4096 -C "github_email@gmail.com"

запускаем ssh-агента

    $ eval "$(ssh-agent -s)"

добавим ключ в ssh-агент

    $ ssh-add ~/.ssh/id_rsa

публичную часть ключа копируем s

    $ cat ~/.ssh/id_rsa.pub

и вносим на github в настройки профиля ssh ans gpg key

![](gitssh-c7cf515e-b2d5-472a-a785-f93c2c6c84b4.png)

проверяем , что получилось

    $ ssh -T git@github.com
    Hi username! You've successfully authenticated, but GitHub does not provide shell access.

# Работа с удаленным репозиторием

Изначально, клонируем репозиторий с github

    git clone link_to_repo_on_github.git


для подтягивания актуальной версии 

    git pull

для отправки своих изменений на github

    git push origin master
