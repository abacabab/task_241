# Струтура каталогов

1) Какая структура каталогов в linux? выведите список файлов в корне системы


```bash
.   bin   dev  home  lib64   lost+found  mnt  proc  run   selinux  sys  usr
..  boot  etc  lib   libx32  media       opt  root  sbin  srv      tmp  var
```
2) Где хранятся папки пользователей в системе?

Хранятся в /home/username/. 

3) Где домашняя папка суперпользователя?

/root/

4) Где хранятся основые конфигурационные файлы в системе?

/etc/ — основная директория конфигов системы и программ
/etc/sysconfig/ или /etc/default/ — конфиги служб (в некоторых дистрибутивах)
/etc/network/, /etc/systemd/, /etc/ssh/ — специфические конфиги

5) ЧТо за папки /bin,/sbin,usr/sbin,/usr/sbin

/bin, /usr/bin — основные исполняемые файлы для всех пользователей
/sbin, /usr/sbin — системные утилиты для администрирования
/usr/local/bin, /usr/local/sbin — программы, установленные администратором вручную