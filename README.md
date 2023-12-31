# Домашнее задание к занятию «Защита сети» - Иванов Игорь

### Подготовка к выполнению заданий

1. Подготовка защищаемой системы:

- установите **Suricata**,
- установите **Fail2Ban**.

2. Подготовка системы злоумышленника: установите **nmap** и **thc-hydra** либо скачайте и установите **Kali linux**.

Обе системы должны находится в одной подсети.

------

### Задание 1

Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

**sudo nmap -sA < ip-адрес >**

В логах ничего нет.

**sudo nmap -sT < ip-адрес >**

![sT](https://github.com/gaming4funNel/sdb-homework-13-03/blob/main/img/sT.png)

В логах записи о сканировании портов с использованием TCP-пакетов.

**sudo nmap -sS < ip-адрес >**

![sS](https://github.com/gaming4funNel/sdb-homework-13-03/blob/main/img/sS.png)

В логах записи о сканировании портов с использованием TCP-пакетов.

**sudo nmap -sV < ip-адрес >**

![sV](https://github.com/gaming4funNel/sdb-homework-13-03/blob/main/img/sV.png)

В логах записи о попытках определения версий сервисов на целевой машине, что может указывать на анализ сервисов и их уязвимостей.

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.


*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*

------

### Задание 2

Проведите атаку на подбор пароля для службы SSH:

**hydra -L users.txt -P pass.txt < ip-адрес > ssh**

1. Настройка **hydra**: 
 
 - создайте два файла: **users.txt** и **pass.txt**;
 - в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.

Дополнительная информация по **hydra**: https://kali.tools/?p=1847.

2. Включение защиты SSH для Fail2Ban:

-  открыть файл /etc/fail2ban/jail.conf,
-  найти секцию **ssh**,
-  установить **enabled**  в **true**.

Дополнительная информация по **Fail2Ban**:https://putty.org.ru/articles/fail2ban-ssh.html.

![fail2ban](https://github.com/gaming4funNel/sdb-homework-13-03/blob/main/img/fail2ban.png)
![suricata](https://github.com/gaming4funNel/sdb-homework-13-03/blob/main/img/suricata.png)

Fail2ban забанил подключение и до и после включения enabled в true в секции ssh.

*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*