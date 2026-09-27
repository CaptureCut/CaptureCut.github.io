---
title: httpx introduction
id: 007
---

# HTTPX (ProjectDiscovery) - заметка

## Цель

Разобрать инструмент `httpx` из экосистемы ProjectDiscovery.

Используется для проверки живых веб-сервисов и сбора базовой информации о них перед дальнейшим анализом.

Типичный пайплайн:

```text
subfinder -> httpx -> nuclei
```

## Что произошло

Во время изучения выяснилось, что в системе установлен не ProjectDiscovery httpx.

Команда:

```bash
which httpx
```

вернула:

```text
/usr/bin/httpx
```

При попытке вывести справку:

```bash
httpx -h
```

появилась ошибка:

```text
Error: Option '-h' requires 2 arguments.
```

Также:

```bash
httpx --version
```

выдало:

```text
Usage: httpx [OPTIONS] URL
Error: No such option: --version
```

Вывод: установлен другой инструмент под названием `httpx` (не ProjectDiscovery).

## Что ещё выяснилось

Go не установлен:

```bash
go version
```

Результат:

```text
Command 'go' not found
```

Также отсутствуют:

```text
subfinder
assetfinder
```

## Что изучить позже

Установить Go:

```bash
sudo apt install golang-go
```

Установить ProjectDiscovery httpx:

```bash
go install github.com/projectdiscovery/httpx/cmd/httpx@latest
```

Проверить:

```bash
httpx -version
```

## Что хочу разобрать после установки

Основные флаги:

```bash
httpx -sc
httpx -title
httpx -tech-detect
httpx -ip
httpx -server
```

Примеры:

```bash
httpx -l hosts.txt -sc
```

```bash
httpx -l hosts.txt -title
```

```bash
httpx -l hosts.txt -tech-detect
```

```bash
httpx -l hosts.txt -sc -title -tech-detect
```

## Итог

Изучение httpx отложено до настройки окружения.

Следующий шаг:
- установить Go;
- установить ProjectDiscovery httpx;
- провести первое практическое знакомство с инструментом.
