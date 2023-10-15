# Урок 2. Механизмы контрольных групп

Задание :
1) запустить контейнер с ubuntu, используя механизм LXC
2) ограничить контейнер 256 Мб ОЗУ и проверить, что ограничение работает
3) добавить автозапуск контейнеру, перезагрузить ОС и убедиться, что контейнер действительно запустился самостоятельно
4) при создании указать файл, куда записывать логи
5) после перезагрузки проанализировать логи

## Установка ЛКС

`sudo apt update`

`apt-get install lxc debootstrap bridge-utils lxc-templates`

`apt-get install lxd-installer`

`lxd init` (Здесь просто нажимаем на Enter что уствновились значения по умолчанию)
![Alt text](/images/image-4.png)
Проверяем

`lxc storage list`
![Alt text](/images/image-5.png)

И создаем контейнер

`sudo apt update`

`lxc-create -n test123 -t ubuntu` --создаем контейнер

`lxc-start -n test123` -- запускаем

`lxc-attach -n test123` -- войдем в него

`free -m` —проверяем пямаять

`exit` -- выходим

`lxc-stop -n test123` - -закрываем
![Alt text](/images/image-6.png)

`nano /var/lib/lxc/test123/config` конфигурация контейнера

`lxc.rootfs.path = dir:/var/lib/lxc/test1234/rootfs` — путь

`lxc.uts.name = test1234` -- имя

Network configuration — Конфегурация сети
.
.

.
`lxc.cgroup2.memory.max = 256M` -- ограничиваем(В режиме Вставка делаем запись)
![Alt text](/images/image-7.png)

Автоматический старт контейнера с системой (добавить в конфиг)
`lxc.start.auto = 1`
![Alt text](/images/image-8.png)
![Alt text](/images/image-9.png)

`lxc-create --name=con1 --template=ubuntu`  создать контейнер с именем con1 по шаблону ubuntu  (без лог-файла)

`lxc-create -n con2 -t ubuntu --logfile=./con2.log` создать контейнер с именем con1 по шаблону ubuntu, назначить лог-файл

Добавляем в конфиг памят и логирование

`lxc.cgroup2.memory.max = 128M`

`lxc.start.auto = 1`

`lxc.log.file = /home/HomeWork02/con1.log`

`lxc.log.level = 1`

`lxc-start con2 --logfile=./con2.log --logpriority=NOTICE` запуск контейнера с логированием
![Alt text](/images/image-10.png)