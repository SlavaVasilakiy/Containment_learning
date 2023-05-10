# ФИ: Василакий Вячеслав. Группа: Программирование 6 | 3325 / 3424 | 21.09.2022. Урок №2

### Урок 2. Механизмы контрольных групп

__Задание 1:__
1) запустить контейнер с ubuntu, используя механизм LXC
2) ограничить контейнер 256 Мб ОЗУ и проверить, что ограничение работает
3) добавить автозапуск контейнеру, перезагрузить ОС и убедиться, что контейнер действительно запустился самостоятельно
4) при создании указать файл, куда записывать логи
5) после перезагрузки проанализировать логи

__Задание 2*:__ настроить автоматическую маршрутизацию между контейнерами. <br>
Адреса можно взять: 10.0.12.0/24 и 10.0.13.0/24.

### Solution:

__Задание 1:__
1) `lxc-create -n test123 -t ubuntu` , `lxc-create -n test321 -t ubuntu`
2) `nano /var/lib/lxc/test123/config`

    ```script
    # Container specific configuration
    lxc.cgroup2.memory.max = 256M
    lxc.start.auto  =  1
    ```

   `nano /var/lib/lxc/test321/config`

   ```script
    # Container specific configuration
    lxc.cgroup2.memory.max = 256M
    lxc.start.auto  =  1
    ```
   
   `free -m` <br>
   
   ![free-m.jpeg](img%2Ffree-m.jpeg)

3) `reboot` , `lxc-info test123`

    ```script
    Name:           test123
     State:          RUNNING
     PID:            1538
     IP:             10.0.12.1
     IP:             10.0.3.238
     Link:           veth1UmfX5
     TX bytes:      3.36 KiB
     RX bytes:      15.50 KiB
     Total bytes:   18.86 KiB
   ```

   `lxc-info test321`
   
    ```script
   Name:           test321
    State:          RUNNING
    PID:            1670
    IP:             10.0.13.1
    IP:             10.0.3.86
    Link:           vethhYIhhU
    TX bytes:      3.50 KiB
    RX bytes:      12.58 KiB
    Total bytes:   16.08 KiB
    ```
   
4) `nano /var/lib/lxc/test123` , `nano /var/lib/lxc/test321`

   ```script
   # Container specific configuration
   lxc.console.logfile = /var/lib/lxc/test123/test123.log    
   lxc.log.level = 5
   lxc.log.file = /var/lib/lxc/test123/test123_error.log
   ```

   ```script
   # Container specific configuration
   lxc.console.logfile = /var/lib/lxc/test321/test321.log    
   lxc.log.level = 5
   lxc.log.file = /var/lib/lxc/test321/test321_error.log
   ```
   
<br>

![log.jpeg](img%2Flog.jpeg)

<br>

__Задание 2*:__  <br>

В хостовой части прописываем маршруты <br>
`ip route add 10.0.12.0/24 via 10.0.3.1 dev lxcbr0` <br>
`ip route add 10.0.13.0/24 via 10.0.3.1 dev lxcbr0` <br>

![ping.jpeg](img%2Fping.jpeg)
