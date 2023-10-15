# Урок 1. Механизмы пространства имен

Задание: необходимо продемонстрировать изоляцию одного и того же приложения (как решено на семинаре - командного интерпретатора) в различных пространствах имен.

## Создание каталогов и копирование необходимых файлов

`mkdir ~/testfolder`

`mkdir ~/testfolder/bin`

`cp /bin/bash ~/testfolder/bin`

`mkdir ~/testfolder/lib ~/testfolder/lib64`

`cp /lib/x86_64-linux-gnu/libtinfo.so.6 ~/testfolder/lib`

`cp /lib/x86_64-linux-gnu/libc.so.6 ~/testfolder/lib`

`cp /lib64/ld-linux-x86-64.so.2 ~/testfolder/lib64/`

## команда `chroot` для изменения корневой папки  текущей среды

`sudo chroot ~/testfolder /bin/bash`

![Alt text](/images/image.png)

## Добавление дополнительных файлов для решения проблемы с отсутствием команды "ls" и других

`cp /bin/ls ~/testfolder/bin/`

`cp /lib/x86_64-linux-gnu/libselinux.so.1 ~/testfolder/lib/`

`cp /lib/x86_64-linux-gnu/libpcre2-8.so.0 ~/testfolder/lib/`

![Alt text](/images/image-1.png)

НЕДОСТАТКИ `chroot` - необходимость копирования файлов.

## Механизм пространста имен лишен этих недостатков и обеспечивает изоляцию процессов.

## Создание пространства имен для Сети:

`ip netns add testns`

Используя команду ip, мы можем выполнить процесс в созданном пространстве имен:

`ip netns exec testns bash`

![Alt text](/images/image-2.png)


## Более Глубокая Изоляция
Применяя дополнительные параметры, мы можем углубить уровень изоляции:
Изоляция по Процессам и Файловой Системе:

`unshare --net --pid --fork --mount-proc /bin/bash`

`ps aux`

unshare Утилита которая позволяет это разграничивать -
--net — ограничевает сетевое пространство имен
ip a
-mount-proc — разграничивает процессы
ps aux
--fork — изолирует память
--pid — изолирует дерево процессов
Формально мы внутри контейнера
ls
ls /
ps aux

![Alt text](/images/image-3.png)