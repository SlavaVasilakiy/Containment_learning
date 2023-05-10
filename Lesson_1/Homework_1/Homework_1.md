# ФИ: Василакий Вячеслав. Группа: Программирование 6 | 3325 / 3424 | 21.09.2022. Урок №1

### Урок 1. Механизмы пространства имен

### Task:
Необходимо продемонстрировать изоляцию одного и того же приложения <br>
(как решено на семинаре - командного интерпретатора) в различных пространствах имен: <br>
<br>
<br>
**Результатом работы будет**: текст объяснения, логи выполнения, история команд и скриншоты <br>
(важно придерживаться такой последовательности). <br>
В названии работы должны быть указаны ФИ, номер группы и номер урока.

### Solution:

`mkdir lesson1` - создаём директорию <br>
`cd lesson1` - переходим в директорию <br>
`mkdir bin lib lib64` создаём директории для будущих операция <br>
`ldd /bin/bash` - просмотр зависимостей <br>
`cp /bin/bash ./bin/` - копирование bash <br>
`cp /lib/x86_64-linux-gnu/libtinfo.so.6 ./lib` - копируем зависимости <br>
`cp /lib/x86_64-linux-gnu/libc.so.6 ./lib` - копируем зависимости <br>
`cp /lib64/ld-linux-x86-64.so.2 ./lib64` - копируем зависимости <br>
`cp /bin/ls bin/` - копирование ls <br>
`ldd /usr/bin/ls` - просотр зависимостей <br>
`cp /lib/x86_64-linux-gnu/libselinux.so.1 lib` - копируем зависимости <br>
`cp /lib/x86_64-linux-gnu/libpcre2-8.so.0 lib` - копируем зависимости <br>
`cd ..` - выходим из директории <br>
`sudo chroot ~/lesson1/` - меняем корень <br>
<br>

![ldd_bin_bash.jpg](img%2Fldd_bin_bash.jpg) <br>
![bash.jpg](img%2Fbash.jpg) <br>
![lib_lib64.jpg](img%2Flib_lib64.jpg) <br>
![tree1.jpg](img%2Ftree1.jpg) <br>
![tree2.jpg](img%2Ftree2.jpg) <br>
![ldd_bin_ls.jpg](img%2Fldd_bin_ls.jpg) <br>
![chroot.jpg](img%2Fchroot.jpg) <br>
<br>

`sudo man unshare` - документация <br>
`sudo unshare --pid --net --fork --mount-proc bash` - pid(изоляция процессов), net(изоляция по сети), <br>
fork(создать новый процесс), mount-proc(монтировать, изолировать) <br>
<br>

![man_unshare.jpg](img%2Fman_unshare.jpg) <br>
![unshare.jpg](img%2Funshare.jpg)
