`mkdir Containment` - создаём папку <br>
`cd Containment/` - переходим в папку <br>
`ldd /bin/bash` - просмотр зависимых файлов <br>
`mkdir bin` - создаём директорию bin <br>
`cp /bin/bash ./bin/` - копируем bash в эту директорию <br>
`mkdir lib lib64` - создаём директории <br>
`cp /lib/x86_64-linux-gnu/libtinfo.so.6 ./lib` - копируем зависимости <br>
`cp /lib/x86_64-linux-gnu/libc.so.6 ./lib` - копируем зависимости <br>
`cp /lib64/ld-linux-x86-64.so.2 ./lib64` - копируем зависимости <br>
`cd ..` - выходим из директории <br>
`sudo chroot Containment /bin/bash` - меняем корень <br>
`exit` - выходим <br>
`ldd /usr/bin/ls` - просмотр зависимых файлов <br>
`cd Containment/` - переходим в папку <br>
`cp /lib/x86_64-linux-gnu/libselinux.so.1 lib` - копируем зависимости <br>
`cp /lib/x86_64-linux-gnu/libpcre2-8.so.0 lib` - копируем зависимости <br>
`cp /bin/ls bin/` - копируем директорию <br>
`cd ..` - выходим из директории <br>
`sudo chroot ~/Containment/` - меняем корень <br>
<br>
<br>
<br>
`sudo man unshare` - документация <br>
`sudo unshare --pid --net --fork --mount-proc bash` - fork(создать новый процесс), <br> 
mount-proc(монтировать, изолировать), net(изоляция по сети), pid(изоляция процессов) <br>
