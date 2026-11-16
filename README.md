# mephi-linux-security-2026

Защита в операционных системах, домашнее задание №1.

Уникальный номер: **М265281**

Система: Debian GNU/Linux 13 (arm64) в VirtualBox. Все команды выполнялись от root в командной строке. Номера строк ниже соответствуют `history.out`.

| Раздел | Что сделано | Команды (history.out) | Файлы |
|---|---|---|---|
| 1. Пользователь | Группа `students`, пользователь `user1` с UID 1234 в этой группе, пароль, смена пароля раз в 90 дней | 1–6 | `passwd`, `group`, `shadow`, `stat.out` |
| 2.1 Файлы set-UID | Поиск всех файлов с битом set-UID | 7–8 | `setuid-files.out` |
| 2.2 Процессы | `user1` запускает `passwd` (ждёт ввода пароля), в это время ищутся процессы с EUID = 0 и RUID ≥ 1000 | 9–12 | `processes.out` |
| 3. set-UID | Копия `cat` в `/home/user1/privcat`, владелец root, бит set-UID. Обычный `cat` не может прочитать `/etc/shadow`, `privcat` может | 13–17 | `stat.out`, `terminal-output.txt` |
| 4. Привилегии | Копия `chown` в `/home/user1/privchown` с capability `cap_chown`. Обычный `chown` от `user1` не может сменить владельца файла root, `privchown` может | 18–24 | `getcap.out`, `stat.out`, `terminal-output.txt` |
| 5. sudo | `user1` может менять системное время: `user1 ALL=(root) NOPASSWD: /usr/bin/date -s *` в `/etc/sudoers`, проверка `visudo -c` | 25–27 | `sudoers` |
| 6. Артефакты | Скриншот, история команд, `stat`, `getcap` | 28–33 | `mephi-screenshot.png`, `history.out`, `stat.out`, `getcap.out` |

`terminal-output.txt` содержит вывод команд из `history.out`.

## Про файл shadow

Файл `shadow` является копией `/etc/shadow`, в которой хеши паролей заменены на `REDACTED`. Репозиторий публичный, и публиковать хеши паролей небезопасно. Остальные поля не изменены, в том числе срок действия пароля `user1` (90 дней):

```
user1:REDACTED:20773:0:90:7:::
```
