# Открываем firewald

1. Удалите iptables и установите firewalld

```bash
sudo service iptables stop
sudo apt-get remove iptables
sudo apt-get update
sudo apt-get install firewalld
sudo systemctl start firewalld
sudo systemctl enable firewalld
```

2. Попробуйте так-же проверить возможность подключения по ssh

возможность осталась

3. Если её нет то откройте порт

если бы не было, надо было бы сделать так:
```bash
sudo firewall-cmd --add-port=205/tcp
```

4. Выведите список открытых портов с помощью firewall-cmd

```bash
firewall-cmd --list-ports
```

5. Можно ли там добавить порты по названию сервиса?

да, можно

6. На вашей Локальной виртуальной машине попробуйте подключиться к серверу samba из предыдущих заданий

```bash
smbclient //localhost/public -N
```

7. Если не получилось то откройте нужные порты

```bash
sudo firewall-cmd --add-service=samba
```

9. Сделайте так чтобы изменения были постоянными

флаг --permanent
```bash
sudo firewall-cmd --add-port=205/tcp --permanent
sudo firewall-cmd --add-service=samba --permanent
```
