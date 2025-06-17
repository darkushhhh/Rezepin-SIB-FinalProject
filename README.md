# Введение

Тестирование информационных систем в рамках выполнения дипломной работы было проведено в период с 10 по 17 июня 2025 года студентом группы **SIB-44**, **Резепиным Николаем Артемовичем**. Основной целью тестирования было выявление уязвимостей в веб-приложениях, доступных по адресу `http://92.51.39.106`, развернутых на портах: `8050` и `7788`. Задача заключалась в оценке уровня защищённости систем и предоставлении рекомендаций по устранению обнаруженных уязвимостей.

Данный отчёт подготовлен на основе результатов тестирования на проникновение, в рамках выполнения дипломной работы по теме **«Track Penetration Testing»**. Тестирование проводилось в режиме **black box**, что означает отсутствие предварительной информации о внутренней структуре систем. Область тестирования (scope) включала:

- Веб-приложение, развернутое на `http://92.51.39.106:8050` (**NetologyVulnApp.com**)
- Веб-приложение, развернутое на `http://92.51.39.106:7788` (**Beemer**)

Целью тестирования было моделирование действий внешнего злоумышленника с использованием общедоступных инструментов и техник, таких как `nmap`, `ZAP`, `Burp Suite`, `sqlmap`, кастомные шеллы и т.д.

Ниже представлена таблица с перечнем обнаруженных уязвимостей и их уровнями риска. Данная таблица наглядно демонстрирует степень уязвимости тестируемых информационных систем.

## Таблица обнаруженных уязвимостей в тестируемых ИС

| №  | Уровень риска | Уязвимость                                  | OWASP                                          | Уязвимая ИС (port) |
|----|---------------|---------------------------------------------|------------------------------------------------|--------------------|
| 1  | Критический   | SQL Injection                               | [A03:2021-Injection](https://owasp.org/Top10/A03_2021-Injection/)                        | 8050, 7788         |
| 2  | Критический   | Command Injection                           | [A03:2021-Injection](https://owasp.org/Top10/A03_2021-Injection/)                          | 7788               |
| 3  | Критический   | Unrestricted File Upload                    | [A05:2021-Security Misconfiguration](https://owasp.org/Top10/A05_2021-Security_Misconfiguration/)          | 8050, 7788         |
| 4  | Высокий       | Path Traversal                              | [A01:2021-Broken Access Control](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)              | 8050, 7788         |
| 5  | Высокий       | Exposed credentials in public GitHub repository | [A07:2021-Identification and Authentication Failures](https://owasp.org/Top10/A07_2021-Identification_and_Authentication_Failures/) | 7788               |
| 6  | Высокий       | Insecure Transmission of Sensitive Data     | [A02:2021-Cryptographic Failures](https://owasp.org/Top10/A02_2021-Cryptographic_Failures/)             | 8050, 7788         |
| 7  | Высокий       | Session Hijacking Attack                    | [A07:2021-Identification and Authentication Failures](https://owasp.org/Top10/A07_2021-Identification_and_Authentication_Failures/) | 8050               |
| 8  | Средний       | Weak Admin Password                         | [A07:2021-Identification and Authentication Failures](https://owasp.org/Top10/A07_2021-Identification_and_Authentication_Failures/) | 8050               |
| 9  | Средний       | Brute Force Attack                          | [A07:2021-Identification and Authentication Failures](https://owasp.org/Top10/A07_2021-Identification_and_Authentication_Failures/) | 8050, 7788         |
| 10 | Средний       | Cross-Site Scripting (XSS)                  | [A03:2021-Injection](https://owasp.org/Top10/A03_2021-Injection/)                          | 8050, 7788         |

___

## Перейти к следующей странице
 
Далее: Этап №1. [**OSINT**](./OSINT.md)

___
