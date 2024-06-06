# S21_Linux. First Project

## Part 1
![img_1.png](img%2Fimg_1.png)

Смотрим версию Ubuntu после установки

(Команда: "cat /etc/issue")

## Part 2
![img_2.png](img%2Fimg_2.png)

Добавляем пользователя new_user
- "useradd new_user -d /home/user -m -G adm -s /bin/bash"

Проверяем добавление:
- "cat /etc/passwd"

## Part 3
### Part 3.1 Part 3.2
![img_3.png](img%2Fimg_3.png)

Зададим название машины вида user-1
- "sudo hostnamectl set-hostname user-1"

Установим время соответсвующее местному времени
- "sudo timedatectl set-timezone Europe/Moscow"

### Part 3.3
![img_4.png](img%2Fimg_4.png)

lo (loopback device) – виртуальный интерфейс, присутствующий по умолчанию в любом Linux. Он используется для отладки сетевых программ и запуска серверных приложений на локальной машине. С этим интерфейсом всегда связан адрес 127.0.0.1. У него есть dns-имя – localhost.

### Part 3.4
![img_5.png](img%2Fimg_5.png)

DHCP - Dynamic Host Configuration Protocol, сетевой протокол, позволяющий сетевым устройствам автоматически получать IP-адрес и другие параметры, необходимые для работы в сети TCP/IP. Данный протокол работает по модели «клиент-сервер».

### Part 3.5
![img_6.png](img%2Fimg_6.png)

Узнали внутренний IP-адрес шлюза, он же ip-адрес по умолчанию: 
 
 - "ip route | grep default"

### Part 3.6

Изменили файл /etc/netplan/*.yaml, применили изменения в netplan, перезагрузились:

![img_7.png](img%2Fimg_7.png)

- "sudo nano /etc/netplan/00-installer-config.yaml"
- "sudo netplan apply"
- "sudo reboot"

### Part 3.7

Проверили внешний и локальный ip шлюза(значения сошлись)

![img_8.png](img%2Fimg_8.png)

Успешно пропинговали 1.1.1.1 и ya.ru без потерь

![img_9.png](img%2Fimg_9.png)

## Part 4
![img_10.png](img%2Fimg_10.png)

## Part 5

Sudo – это утилита для операционных систем семейства Linux, позволяющая пользователю запускать программы с привилегиями другой учётной записи, как правило, суперпользователя.

![img_11.png](img%2Fimg_11.png)

- "su new_user" переключение на пользователя
- "sudo usermod -aG sudo new_user" добавление в группу sudo

