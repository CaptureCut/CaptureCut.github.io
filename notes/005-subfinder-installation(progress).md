005 - Subfinder

Цель:
Установить и протестировать Subfinder в Kali Linux.

Проверка:

subfinder -version

Результат:

Command 'subfinder' not found

Попытка установки:

sudo apt install subfinder

Результат:

Unable to locate package subfinder

Проверка Go:

go version

Результат:

Command 'go' not found

Попытка установки Go:

sudo apt install golang-go

Результат:

Unable to locate package golang-go

Проверка репозиториев:

cat /etc/apt/sources.list.d/kali.sources

Конфигурация присутствует.

Проверка обновления пакетов:

sudo apt update

Результат:

Could not connect to mirror.wane.kr
Connection refused

Вывод:

Проблема связана с зеркалом Kali.
Установка Subfinder отложена.

Статус:

IN PROGRESS

Следующие шаги:

- разобраться с mirror.wane.kr
- восстановить работу apt
- установить Go
- установить Subfinder
- провести первое тестирование
