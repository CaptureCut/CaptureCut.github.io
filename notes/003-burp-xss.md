---
title: Research Note #003
layout: page
---

Research Note #003 - Reflected XSS (Burp Lab Task #001)

Overview:
Первая собственная веб‑задача для практики Burp Suite. Цель — создать минимальную уязвимую страницу, воспроизвести атаку, понять механику XSS и оформить разбор. Задача локальная, запускается в Kali, решается через Burp Suite.

Task Description:
Мини‑страница принимает параметр msg через GET и выводит его в DOM. Есть наивный фильтр, который заменяет только первый символ "<" на "&lt;", но не защищает от XSS. Это создаёт DOM‑based reflected XSS.

Vulnerable Code (index.html):
```
{% raw %}
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Feedback</title>
</head>
<body>
<h2>Feedback Form</h2>

<form method="GET" action="">
<input type="text" name="msg" placeholder="Your message">
<button type="submit">Send</button>
</form>

<p>Your message:</p>
<div id="output"></div>

<script>
const params = new URLSearchParams(window.location.search);
let msg = params.get("msg") || "";

msg = msg.replace("<", "&lt;");

document.getElementById("output").innerHTML = msg;
</script>
</body>
</html>
{% endraw %}

How to Run (Kali):
Запуск локального сервера:
python3 -m http.server 8080

Открыть страницу:
http://localhost:8080/index.html

Перехватить запросы через Burp Suite и менять параметр msg.

Exploitation (Burp Suite):

Payload 1:
{% raw %}
"><img src=x onerror=alert(1)>
{% endraw %}
```
Причина:
Фильтр заменяет только первый "<". Строка закрывает атрибут, вставляет img, срабатывает onerror.

Payload 2:
```
{% raw %}
<scr<script>ipt>alert(1)</scr<script>ipt>
{% endraw %}
```
Причина:
Фильтр заменяет только первое "<". Вложенные теги остаются. Браузер склеивает теги и выполняет JS.

Why It Works:

innerHTML вызывает интерпретацию HTML. Любые теги и события выполняются.

replace("<", "&lt;") бесполезен:
- заменяет только первое вхождение
- не заменяет ">"
- не заменяет кавычки
- не заменяет атрибуты
- не заменяет события
- не заменяет вложенные теги

DOM‑based XSS:
Уязвимость возникает в браузере, а не на сервере. Параметр читается через JS и вставляется в DOM.

Fix:

Безопасный вывод:
textContent вместо innerHTML.

Полная экранизация:
замена &, <, >, ", '.

CSP:
script-src 'self'.

Notes:
Эта задача закрывает пробелы, которые возникли в University CTF 2025. XSS — это не только <script>alert(1)</script>. Наивные фильтры легко обходятся. Burp Suite удобен для перехвата и модификации параметров.

