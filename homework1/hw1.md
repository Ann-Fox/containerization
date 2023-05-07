
Чернышева Анна 
ЦП | Разработчик. Программист | 3416 | 2

# Контейнеризация (семинары)
## Урок 1. Механизмы пространства имен
### Задание: необходимо продемонстрировать изоляцию одного и того же приложения (как решено на семинаре - командного интерпретатора) в различных пространствах имен.

Формат сдачи ДЗ: предоставить доказательства выполнения задания посредством ссылки на google-документ с правами на комментирование/редактирование.
Результатом работы будет: текст объяснения, логи выполнения, история команд и скриншоты (важно придерживаться такой последовательности).
В названии работы должны быть указаны ФИ, номер группы и номер урока.


1. Создать директорию

    annfox@WIN-ITTRKFDRUUI:/home$ cd annfox/

    annfox@WIN-ITTRKFDRUUI:~$ ls

    ann-fox.github.io  backup-1677426142.tar  geekbrains  testproject

    annfox@WIN-ITTRKFDRUUI:~$ mkdir testfolder

    annfox@WIN-ITTRKFDRUUI:~$ ls

    ann-fox.github.io  backup-1677426142.tar  geekbrains  testfolder  testproject



2. Создать каталог bin в testfolder

    annfox@WIN-ITTRKFDRUUI:~$ mkdir testfolder/bin

    annfox@WIN-ITTRKFDRUUI:~$ ls

    ann-fox.github.io  backup-1677426142.tar  geekbrains  testfolder  testproject

    annfox@WIN-ITTRKFDRUUI:~$ cd testfolder/

    annfox@WIN-ITTRKFDRUUI:~/testfolder$ ls

    bin


3. Скопировать исполняемый файл bash в каталог testfolder/bin

    annfox@WIN-ITTRKFDRUUI:~/testfolder$ cd ..

    annfox@WIN-ITTRKFDRUUI:~$ cp /bin/bash testfolder/bin

    annfox@WIN-ITTRKFDRUUI:~$ cd testfolder/bin/

    annfox@WIN-ITTRKFDRUUI:~/testfolder/bin$ ls

    bash


    annfox@WIN-ITTRKFDRUUI:~$ chroot testfolder

    chroot: cannot change root directory to 'testfolder': Operation not permitted


4. Просмотреть необходимые библиотеки для bin

    annfox@WIN-ITTRKFDRUUI:~$ ldd /bin/bash
        linux-vdso.so.1 (0x00007ffd6ebb8000)
        libtinfo.so.6 => /lib/x86_64-linux-gnu/libtinfo.so.6 (0x00007f24f96f7000)
        libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f24f94cf000)
        /lib64/ld-linux-x86-64.so.2 (0x00007f24f9891000)


5. Создать каталоги lib и lib64

    annfox@WIN-ITTRKFDRUUI:~$ mkdir testfolder/lib

    annfox@WIN-ITTRKFDRUUI:~$ mkdir testfolder/lib64

    annfox@WIN-ITTRKFDRUUI:~$ cd testfolder/

    annfox@WIN-ITTRKFDRUUI:~/testfolder$ ls

    bin  lib  lib64


6. Копировать библиотеки в home_work1

    annfox@WIN-ITTRKFDRUUI:~/testfolder$ cp /lib/x86_64-linux-gnu/libtinfo.so.6 ./lib

    annfox@WIN-ITTRKFDRUUI:~/testfolder$ cp /lib/x86_64-linux-gnu/libc.so.6 ./lib

    annfox@WIN-ITTRKFDRUUI:~/testfolder$ cp /lib64/ld-linux-x86-64.so.2 ./lib64/

    annfox@WIN-ITTRKFDRUUI:~/testfolder$ ls

    bin  lib  lib64

    annfox@WIN-ITTRKFDRUUI:~/testfolder$ cd lib

    annfox@WIN-ITTRKFDRUUI:~/testfolder/lib$ ls

    libc.so.6  libtinfo.so.6

    annfox@WIN-ITTRKFDRUUI:~/testfolder/lib$ cd ..

    annfox@WIN-ITTRKFDRUUI:~/testfolder$ cd lib64

    annfox@WIN-ITTRKFDRUUI:~/testfolder/lib64$ ls

    ld-linux-x86-64.so.2


7. Смена корня

    annfox@WIN-ITTRKFDRUUI:~$ sudo chroot testfolder

    [sudo] password for annfox:

    bash-5.1#

    bash-5.1#

    bash-5.1#

    bash-5.1#

    bash-5.1#

    bash-5.1#

    bash-5.1# ls

    bash: ls: command not found

    bash-5.1# exit
    
    exit

![Result1](.//images/scr1.jpg)

![Result2](.//images/scr2.jpg)
