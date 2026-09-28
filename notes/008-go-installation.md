---
title: go-installation
id: 008
---

# 008. Установка и проверка Go в Kali Linux

Дата: 2026-09-27

## Цель

Установить Go для разработки собственных инструментов и экспериментов.

## Первоначальная проблема

Попытка установки через APT завершалась ошибкой:

```bash
sudo apt install golang-go -y
```

Ошибка:

```text
Unable to locate package golang-go
```

## Диагностика

Проверено состояние репозиториев:

```bash
sudo apt update
```

Обновление индексов прошло успешно.

Выяснилось, что в системе используется новый формат конфигурации APT:

```bash
/etc/apt/sources.list.d/kali.sources
```

Файл:

```bash
cat /etc/apt/sources.list.d/kali.sources
```

Содержал корректный репозиторий Kali Rolling.

Также отсутствует старый файл:

```bash
/etc/apt/sources.list
```

что является нормальным для современных версий Kali Linux.

## Решение

Установлена официальная версия Go:

```bash
go1.25.1
```

Добавлен Go в PATH:

```bash
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.zshrc
source ~/.zshrc
```

## Проверка установки

Проверка версии:

```bash
go version
```

Результат:

```text
go version go1.25.1 linux/amd64
```

Проверка расположения исполняемого файла:

```bash
which go
```

Результат:

```text
/usr/local/go/bin/go
```

## Проверка компиляции

Создан тестовый файл:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello from Kali")
}
```

Сборка:

```bash
go build hello.go
```

Получен исполняемый файл:

```text
hello
```

Запуск:

```bash
./hello
```

Результат:

```text
Hello from Kali
```

## Дополнительная диагностика

Установлен и проверен strace:

```bash
sudo apt install strace
```

Трассировка процесса сборки:

```bash
strace -f -o trace.log go build hello.go
```

Лог успешно создан:

```text
trace.log
```

Проверка внутреннего процесса сборки Go:

```bash
go build -x -work hello.go
```

## Итог

- Go успешно установлен.
- Go добавлен в PATH.
- Компиляция работает.
- Исполняемые файлы создаются и запускаются.
- strace работает и может использоваться для исследования процесса сборки.

Версия Go: `1.25.1`

Статус: **DONE**
