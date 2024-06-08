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
![img_6.1.png](img%2Fimg_6.1.png)

Узнали внутренний IP-адрес шлюза, он же ip-адрес по умолчанию: 
 - "ip route | grep default"

Узнали внешний IP-адрес шлюза: 
 - "ping -c 1 8.8.8.8 | grep PING | awk '{print $3}' | tr -d '()'"

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

 ## Part 9

 ![img_28.png](img%2Fimg_28.png)

<b>Вывод команды top:<b>

- Uptime: 25 минут
- Пользователей: 1
- Загрузка системы: 0,00, 0,00, 0,00
- Процессы: 102 (1 запущенный, 101 в ожидании)
- Загрузка CPU: 0,0% пользовательского времени, 0,0% системного времени, 100% простаивание
- Память: 1971,4 MiB всего, 1465,4 MiB свободно, 148.8 MiB использовано

<b>Использование команды **htop**<b>

fn + F6-открыть сортировкe

 - отсортированному по PID
  
 ![img_29.png](img%2Fimg_29.png)

- отсортированному по PERCENT_CPU

 ![img_30.png](img%2Fimg_30.png)

- отсортированному по PERCENT_MEM
  
 ![img_31.png](img%2Fimg_31.png)

- отсортированному по TIME
  
 ![img_32.png](img%2Fimg_32.png)

fn + F4 для фильтрации

- отфильтрованному для процесса sshd 
  
 ![img_33.png](img%2Fimg_33.png)

fn + F3 для поиска

- с процессом syslog, найденным, используя поиск
  
 ![img_34.png](img%2Fimg_34.png)

fn + F2 

- с добавленным выводом hostname, clock и uptime<br>

    ![img_35.png](img%2Fimg_35.png)


 ## Part 10

Жесткий диск:

- Название: /dev/sda
- Размер: 10 ГБ (гигабайт), что равно 10737418240 байтам.
- Количество секторов: 20971520. 

Разделы:
- /dev/sda1:
Размер: 1 МБ (мегабайт)
Начальный сектор: 2048, Конечный сектор: 4095.
- /dev/sda2:
Размер: 1,8 ГБ (гигабайт)
Начальный сектор: 4096, Конечный сектор: 3674111.
- /dev/sda3:
Размер: 8,3 ГБ (гигабайт)
Начальный сектор: 3674112, Конечный сектор: 20969471.
 

![img_36.png](img%2Fimg_36.png)
![img_37.png](img%2Fimg_37.png)

## Part 11

Из вывода команды df для корневого раздела (/) следующая информация:

- Размер раздела: 8,408,452 килобайт
- Размер занятого пространства: 4,246,544 килобайт
- Размер свободного пространства: 3,713,192 килобайт
- Процент использования: 54%.
- Единица измерения в выводе - килобайты (1K-blocks).

![img_38.png](img%2Fimg_38.png)

Для корневого раздела (/) из df -Th следующие данные:

- Размер раздела: 8,1G
- Размер занятого пространства: 4,1G
- Размер свободного пространства: 3,6G
- Процент использования: 54%
- Тип файловой системы: tmpfs
![img_39.png](img%2Fimg_39.png)

## Part 12

- ``du``
![img_40.png](img%2Fimg_40.png)

 - ``du -h``

![img_41.png](img%2Fimg_41.png)

 - ``du /home -h``

![img_42.png](img%2Fimg_42.png)

 - ``du /var -h``

![img_43.png](img%2Fimg_43.png)

 - ``sudo du /var/log -h``

![img_44.png](img%2Fimg_44.png)

 - ``sudo du /var/log/* -h``

![img_45.png](img%2Fimg_46.png)


## Part 13

  - ``ncdu ``

![img_46.png](img%2Fimg_46.png)

  - ``ncdu /home``

![img_47.png](img%2Fimg_47.png)

  - ``ncdu /var``

![img_48.png](img%2Fimg_48.png)

 - ``ncdu /var/log``

![img_49.png](img%2Fimg_49.png)

## Part 14
<b>Последняя авторизация<b>

![img_50.png](img%2Fimg_50.png)

<b>Перезапуск OpenSSH Server<b>

![img_51.png](img%2Fimg_51.png)


## Part 15

- ``crontab -e``
![img_52.png](img%2Fimg_52.png)

- ``grep CRON /var/log/syslog``

![img_53.png](img%2Fimg_53.png)

- ``crontab -l``
![img_54.png](img%2Fimg_54.png)

Удаление задач:
- ``crontab -r``
- ``crontab -l``

![img_55.png](img%2Fimg_55.png)