
# Шарим


1. Установите пакет samba

```bash
apt-get install samba
```

2. ЧТо такое побщая папка, зачем оно может быть нужно?

Общая папка - сетевой ресурс, доступный другим компьютерам по протоколу SMB/CIFS. 
Нужно для:
- Обмена файлами в локальной сети
- Доступа к файлам с Windows-машин
- Сетевых хранилищ (NAS)
- Резервного копирования

3. Создайте общую папку без пароля с правами только на чтение файлов

```bash
mkdir -p /samba/public
chmod 777 /samba/public
```
В файл /etc/samba/smb.conf в конец добавил
```bash
[public]
    path = /samba/public
    browseable = yes
    read only = yes
    guest ok = yes
```
```bash
systemctl restart smb nmb
```

4. Создайте общую папку с паролем с правами на чтение и запись

```bash
mkdir -p /samba/private
```
В файл /etc/samba/smb.conf в конец добавил
```bash
[private]
    path = /samba/private
    browseable = yes
    read only = no
    valid users = arix
```
```bash
systemctl restart smb nmb
```

5. Создайте общую папку с доступом для какой-то группы с полными правами

```bash
mkdir -p /samba/group
groupadd samba_group
usermod -aG samba_group arix
```
В файл /etc/samba/smb.conf в конец добавил
```bash
[group_share]
    path = /samba/group
    browseable = yes
    read only = no
    valid users = @samba_group
```
```bash
systemctl restart smb nmb
```

6. Создайте общую папку в которой у одной группы будет полный доступ, а у другой только доступ на чтение.
Третья группа не должна иметь к ней доступа

```bash
groupadd full_access_group
groupadd read_only_group
groupadd no_access_group
```

```bash
[multi_group]
    path = /samba/multi
    browseable = yes
    read only = no
    valid users = @full_access_group, @read_only_group
    write list = @full_access_group
    invalid users = @no_access_group
```
```bash
systemctl restart smb nmb
```