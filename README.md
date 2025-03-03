# TI knowledge base compiled by @s0ld13r



## C2 fingerprinting

Что такое C2 fingerprinting? 

C2 fingerprinting — это процесс **идентификации и распознавания командно-контрольных серверов (Command and Control, C2)** по их уникальным характеристикам, сетевым артефактам или поведенческим особенностям.

### Зачем это нужно?

- Помогает **обнаруживать** инфраструктуру атакующих (APT-групп, киберпреступников).
- Позволяет **распознавать** конкретные фреймворки, например, Cobalt Strike, Sliver, Mythic, Metasploit.
- Упрощает **автоматический анализ трафика и выявление угроз** на ранних стадиях.
### На что смотрят при C2 fingerprinting?

| Категория                  | Примеры артефактов                                                                       |
| -------------------------- | ---------------------------------------------------------------------------------------- |
| **SSL/TLS сертификаты**    | `issuer.cn`, `subject.cn`, уникальные поля, самоподписанные сертификаты (как у AsyncRAT) |
| **HTTP-заголовки**         | Уникальные заголовки или их отсутствие, поведение при 404, user-agent                    |
| **Иконки (favicons)**      | Хэши иконок веб-интерфейса (например, Metasploit favicon hash)                           |
| **Формат трафика**         | Особенности запросов и ответов — нестандартные заголовки, шифрование, разделители        |
| **Доменные шаблоны**       | Используемые генераторы доменов (DGA) или паттерны имен                                  |
| **Ответы сервера**         | Специфичные ошибки или ответы, например, при попытке обращения к несуществующему ресурсу |
| **Иконки, титулы страниц** | Как у Mythic или Supershell — заголовок страницы (title) или hash favicon                |
###  FOFA queries

| Малварь / C2      | Параметры                                                |
|------------------|--------------------------------------------------|
| **AsyncRAT**        | `cert.subject.cn="AsyncRAT Server"`<br>`cert.issuer.cn="AsyncRAT Server"` |
| **Cobalt Strike**   | `cert.issuer.cn="Major Cobalt Strike"`<br>`cert.issuer.org="cobaltstrike"` |
| **Amadey Bot**      | `cert.subject.cn="desas.digital"` |
| **Quasar RAT**      | `cert.subject.cn="Quasar Server CA"` |
| **Laplas Clipper**  | `cert.subject.cn="Laplas.app"`<br>`icon_hash="1123908622"` |
| **Sliver C2**       | `cert.subject.cn="multiplayer"`<br>`cert.issuer.cn="operators"` |
| **Mythic C2**       | `icon_hash="-859291042"`<br>`title=="Mythic"` |
| **Supershell Botnet** | `icon_hash="-1010228102"`<br>`title="Supershell"` |
| **DC RAT**          | `cert.issuer.cn="DcRat Server"` |
| **Metasploit C2**   | `http.favicon.hash:-127886975` |

### Полезные репозитории

[RATandC2](https://github.com/RATandC2) - коллекция утилит для удаленного доступа и форки C2, полезно для изучения исходного кода и поиска оригинальных имплантов.

[awesome-rat](https://github.com/alphaSeclab/awesome-rat) - репозиторий с ссылками на исследования RAT и исходным кодом.
