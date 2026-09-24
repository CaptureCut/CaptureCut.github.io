---
title: Research Note #003
layout: page
---

Research Note #003 — Reflected XSS (Burp Lab Task #001)

Overview:
Первая собственная веб‑задача для практики Burp Suite. Цель — создать минимальную уязвимую страницу, воспроизвести атаку, понять механику XSS и оформить разбор. Задача локальная, запускается в Kali, решается через Burp Suite.

Task Description:
Мини-страница принимает параметр msg через GET и выводит его в DOM. В коде используется innerHTML и наивная фильтрация "<", что приводит к DOM-based XSS.

Полный HTML-код задачи находится в репозитории:
lab/xss/001-basic-reflected/index.html

Vulnerable Fragment:
Фрагмент уязвимого кода:

msg = msg.replace("<", "&lt;");
document.getElementById("output").innerHTML = msg;

How to Run (Kali):
Запуск локального сервера:
python3 -m http.server 8080

Открыть страницу:
http://localhost:8080/index.html

Перехватить запросы через Burp Suite и менять параметр msg.

Exploitation (Burp Suite):

Payload 1:
"><img src=x onerror=alert(1)>

Причина:
Фильтр заменяет только первый "<". Строка закрывает атрибут, вставляет img, срабатывает onerror.

Payload 2:
<scr<script>ipt>alert(1)</scr<script>ipt>

Причина:
Фильтр заменяет только первое "<". Вложенные теги остаются. Браузер склеивает теги и выполняет JS.

Why It Works:
innerHTML вызывает интерпретацию HTML. Наивная фильтрация не защищает от XSS.

Проблемы фильтра:
- заменяет только первое вхождение "<"
- не заменяет ">"
- не заменяет кавычки
- не заменяет атрибуты
- не заменяет события
- не заменяет вложенные теги

DOM-based XSS возникает в браузере, а не на сервере: параметр читается через JS и вставляется в DOM.

Fix:
- использовать textContent вместо innerHTML
- полная экранизация &, <, >, ", '
- CSP: script-src 'self'

Notes:
Эта задача закрывает пробелы, возникшие в University CTF 2025. XSS — это не только <script>alert(1)</script>. Наивные фильтры легко обходятся. Burp Suite удобен для перехвата и модификации параметров.

