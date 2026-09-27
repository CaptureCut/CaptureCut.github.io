---
title: go-installation
id: 008
---

008. Установка Go в Kali Linux

Дата: 2026-09-27

Цель:
Установить Go для разработки собственных инструментов и экспериментов.

Проблема:
Команда установки через APT не работала:

sudo apt install golang-go -y

Ошибка:

Unable to locate package golang-go

Проверка показала, что репозиторий Kali настроен корректно, однако пакеты Go отсутствовали в локальном индексе APT.

Решение:
Установлена официальная версия Go.

Добавлен Go в PATH:

echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.zshrc
source ~/.zshrc

Проверка:

go version

Результат:

go version go1.25.1 linux/amd64

Дополнительная проверка:

which go

Результат:

/usr/local/go/bin/go

Итог:
Go успешно установлен и доступен из терминала.

Версия:
go1.25.1

Статус:
DONE
