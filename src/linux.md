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

## Part 6

Эти команды запустят службу и включат ее для автоматического запуска при каждом старте системы.

 - "sudo apt install systemd-timesyncd"

 - "sudo systemctl start systemd-timesyncd"
AND
 - "sudo systemctl enable systemd-timesyncd"

 Убедитесь, что служба работает без ошибок:

 - "sudo systemctl status systemd-timesyncd"

![img_12.png](img%2Fimg_12.png)

 ## Part 7
### Part 7.1

**VIM** Для сохранения и выхода нажал ESC и прописал :w :q

![img_13.png](img%2Fimg_13.png)


**NANO** Для сохранения нажал ^X далее Yes и название файла

![img_14.png](img%2Fimg_14.png)

**JOE** Для сохранения и выхода нажал ^KX

![img_15.png](img%2Fimg_15.png)

### Part 7.2

**VIM** Для выхода без сохранения ESC -> :q! -> ENTER

![img_16.png](img%2Fimg_16.png)

**NANO** Для выхода без сохранения ^X -> N

![img_17.png](img%2Fimg_17.png)

**JOE** Для выхода без сохранения ^C -> y

![img_18.png](img%2Fimg_18.png)

### Part 7.3

**VIM** Для поиска: /что_ищем

![img_19.png](img%2Fimg_19.png)

**VIM** Для замены: :s/что_заменить/чем

![img_20.png](img%2Fimg_20.png)

**NANO** Для поиска: ^W -> что ищем

![img_21.png](img%2Fimg_21.png)

**NANO** Для замены: ^\ -> что заменить -> чем -> Y

![img_22.png](img%2Fimg_22.png)

**JOE** Для поиска: ^K F -> что ищем -> I

![img_23.png](img%2Fimg_23.png)

**JOE** Для замены: ^K F -> что заменить -> R -> чем -> Y

![img_24.png](img%2Fimg_24.png)


 ## Part 8

![img_25.png](img%2Fimg_25.png)

- sudo systemctl enable ssh - запуск системы ssh
- sudo nano /etc/ssh/sshd_config - Port 2022
- sudo systemctl restart sshd

![img_26.png](img%2Fimg_26.png)
- Отображение процесса
- ps - выводит сведения о процессах в статическом виде
- -е - выбор всех процессов
- | grep sshd - поиск через pipe как вывод грепа для ввода ps

- "sudo reboot"
- "netstat -tan"
![img_27.png](img%2Fimg_27.png)
- tan:
- t - отабражает TCP подключения
- a - Показать состояние всех сокетов; обычно сокеты, используемые серверными процессами не показываются
- n - Показать сетевые адреса как числа. netstat обычно показывает адреса как символы

| Атрибут       | Описание                |
| ------------- |:------------------|
| Proto     | Содержит тип протокола    |
| Recv-Q     | Счетчик байтов не скопированных программой пользователя их этого сокета |
| Send-Q  | Счетчик байтов, не подтвержденных удалленым узлом         |
| Local address  | Адрес и номер порта локального конца сокета        |
| Foreign address  | Адрес и номер порта удаленного конца сокета        |
| State  | Состояние сокета        |
