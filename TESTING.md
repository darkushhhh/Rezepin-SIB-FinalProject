# Этап №3. Testing

## Вводная информация

На предыдущем этапе было проведено сканирование двух целевых веб-приложений — `NetologyVulnApp.com (8050)` и `Beemer (7788)`, в результате которого были выявлены основные уязвимости, ставшие основой для дальнейшего ручного Penetration testing.

Однако полученный перечень уязвимостей не является исчерпывающим, также дополнительно будут исследованы потенциальные уязвимости, которые могли быть пропущены автоматическими сканерами.

Основными источниками информации для тестирования послужили:
- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP Cheat Sheets](https://cheatsheetseries.owasp.org/)
- [Книга Андрея Бирюкова «Информационная безопасность. Защита и нападение»](https://dmkpress.com/catalog/computer/securuty/978-5-93700-219-8/?srsltid=AfmBOopHiNlFCvwZMa-awRfJnO7HYnrBu95LsXbc_cnN_9TyI6LgVBV3)

### Таблица с обнаруженными уязвимостями по OWASP Top 10
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

---
