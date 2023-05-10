`apt install cgroup-tools` - установка утилиты позволяющей использовать cGroups <br>
`ll /sys/fs/cgroup/` - директория где хранятся все cGroups <br>
`mkdir test_cgroup` - в данном случае это создание cGroup сразу с файловой системой <br>
`cgcreate -a root -g memory:test_cgroup2` - создание с указанием кому будет принадлежать и с какими ограничениями, <br>
после двоеточия указывается название группы <br>
`cd test_cgroup/` - переход в директорию <br>

<br>
<br>

`sudo unshare --fork --pid --mount-proc bash` - запускаем изолированный bash <br>
`watch -n 0.2 free -h` - запуск мониторинга с обновлением в 0,2 сек <br>
`nano mem_generator.py` - открываем редактор для создания скрипта <br>

```python
#!/bin/python3
list = ['']
i = 0
while True:
    list.append(i)
    i = i + 1
```

<br>

`chmod +x mem_generator.py` - Для того чтобы запускать скрипт <br>
`./mem_generator.py` - запуск <br>
`cgcreate -a root -g memory:my_cgroup1` - Создаем cgroup <br>
`cd /sys/fs/cgroup/my_cgroup1/` <br>
`cd /sys/fs/cgroup/` <br>
`echo 512M > /sys/fs/cgroup/my_cgroup1/memory.max` - выставим ограничение оперативной памяти в 512М <br>
`echo 512M > /sys/fs/cgroup/my_cgroup1/memory.swap.max` - ограничение файла подкачки <br>
`cat /sys/fs/cgroup/my_cgroup1/memory.max` - прочитаем значение <br>
`cgexec -g memory:my_cgroup1 /bin/bash` - выполняем запуск программы баш с учетом лимитов <br>
`cgexec -g memory:my_cgroup1 unshare -m -p -f --mount-proc  /bin/bash` - запуск контейнера с лимитами <br>

<br>
<br>

`apt install lxc` - установка утилиты <br>
`apt install lxc-utils` - установка дополнений <br>
`apt install lxc-templates` - установка дополнений <br>
`apt install lxd-installer` - установка менеджера демонов <br>
`systemctl status lxc` - статус демона <br>
`lxc storage list` - смотрим списки <br>
`lxc network list` <br>
`lxc remote list` <br>
`lxc image list images: | more` - список доступных имейджев с репозитория <br>
`cat /etc/default/lxc-net` - настройки сети <br>
`cat /etc/lxc/default.conf ` <br>
`ip a` - напоследок обязательно <br>

<br>

Для начала необходимо повторить задание лекции: создать контейнер, сделать ему ограничение в 256 Мб ОЗУ. <br>
`lxc-create -n test123 -t ubuntu` <br>
`lxc-ls --fancy` <br>
`lxc-stop -n test123` <br>
`nano /var/lib/lxc/test123/config` <br>

```script
# Container specific configuration
lxc.cgroup2.memory.max = 256M
lxc.start.auto  =  1
```

```script
# Network configuration
lxc.net.0.ipv4.address = 10.0.12.1/24
lxc.net.0.ipv4.gateway = 10.0.3.1
```

`lxc-ls -f` - снаружи контейнера <br>
`free -m` - внутри контейнера <br>
`cd /var/lib/lxc` - директория lxc контейнеров <br>
`lxc-start -n test123` - старт <br>
`lxc-attach -n test123` - вход в контейнер <br>
`lxc-stop -n test123` - стоп <br>
`lxc-info -n test123` - узнать информацию о контейнере <br>
`cat /etc/default/lxc-net` - настройки сети <br>
`ip route add 10.0.13.0/24 via 10.0.12.1` - внутри контейнера <br>

`nano /var/lib/lxc/test123/config` <br>

```script
# Container specific configuration
lxc.logfile = /var/log/lxc/mycontainer.log
```

для логирования




