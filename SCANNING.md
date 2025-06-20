# Этап №2. Scanning

## Инструменты Scanning

Для анализа целевого IP-адреса и портов, на которых развернуты веб-приложения, были использованы open-source инструменты, предназначенные для выявления уязвимых сервисов, автоматического обнаружения известных уязвимостей в веб-приложениях, а также поиска скрытых файлов, директорий, поддоменов и других ресурсов веб-сервера, не отображаемых явно на сайте.

**Инструменты и их функционал:**
- [Nmap](https://nmap.org) : Сканирование сети и портов для обнаружения активных хостов, открытых портов и запущенных сервисов.
- [Nikto](https://github.com/sullo/nikto) : Сканирование веб-серверов для выявления уязвимостей, конфигурационных ошибок и потенциально опасных файлов.
- [Gobuster](https://github.com/OJ/gobuster) : Перечисление скрытых директорий, файлов и поддоменов веб-сервера.
- [FFUF](https://github.com/ffuf/ffuf) : Быстрое сканирование веб-ресурсов для обнаружения скрытых файлов, директорий и параметров.
- [ZAP](https://www.zaproxy.org) : Автоматизированное тестирование веб-приложений на наличие уязвимостей.

___

## 1. Сканирование с использованием Nmap

### NetologyVulnApp.com (8050)

**Цель:**  
- веб-приложение, доступное по адресу `92.51.39.106:8050`

**Конфигурация:**  
```
nmap -A -sV --version-all -O -p 8050 --reason -T4 --defeat-rst-ratelimit 92.51.39.106
```

**Результаты сканирования:**  
<details>
<summary>screenshot Nmap(8050)</summary>
 
![](screenshots/SCANNING/nmap/nmap_8050.png)

</details>

**Вывод:**  
Сканер Nmap подтвердил данные, ранее полученные с помощью инструмента Censys Search, относительно конфигурации сервиса, развернутого на порте `8050`.

Полная версия отчета Nmap (8050) - [NmapReport_8050](reports/nmap/nmap_report.txt)

___

### Beemer (7788)

**Цель:**  
- веб-приложение, доступное по адресу `92.51.39.106:7788`

**Конфигурация:**  
```
nmap -A -sV --version-all -O -p 7788 --reason -T4 --defeat-rst-ratelimit 92.51.39.106
```

**Результаты сканирования:**  
<details>
<summary>screenshot Nmap(7788)</summary>
 
![](screenshots/SCANNING/nmap/nmap_7788.png)

</details>

**Вывод:**  
Сканер Nmap подтвердил данные, ранее полученные с помощью инструмента ZoomEye, относительно конфигурации сервиса, развернутого на порте `7788`.  

Также сканером Nmap был просканирован весь целевой адрес `92.51.39.106`, на наличие других, ранее не обнаруженных портов, но конкретных результатов это не дало.  
Предполагается, что на хосте установлена система предотвращения вторжений, которая и блокирует попытку более глубинного сканирования.

Полная версия отчета Nmap (7788) - [NmapReport_7788](reports/nmap/nmap_report.txt)

___

## 2. Сканирование с использованием Nikto

### NetologyVulnApp.com (8050)

**Цель:**  
- веб-приложение, доступное по адресу `92.51.39.106:8050`

**Конфигурация:**  
```
nikto -host http://92.51.39.106:8050 -output output.html -Format htm
```

**Результаты сканирования:**  
<details>
<summary>screenshot Nikto(8050)</summary>
 
![](screenshots/SCANNING/nikto/nikto_8050.png)

</details>

**Вывод:**  
Сканер Nikto выявил ряд уязвимостей в веб-приложениях, варьирующихся от незначительных до потенциально критических. Однако для подтверждения их наличия и исключения ложноположительных результатов требуется проведение ручного тестирования.  

Полная версия отчета Nikto (8050) - [NiktoReport_8050](reports/nikto/8050_nikto_report.html)

___

### Beemer (7788)

**Цель:**  
- веб-приложение, доступное по адресу `92.51.39.106:7788`

**Конфигурация:**  
```
nikto -host http://92.51.39.106:7788 -output output.html -Format htm
```

**Результат:**  
<details>
<summary>screenshot Nikto(7788)</summary>
 
![](screenshots/SCANNING/nikto/nikto_7788.png)

</details>

**Вывод:**  
Сканер Nikto выявил ряд уязвимостей в веб-приложениях, варьирующихся от незначительных до потенциально критических. Однако для подтверждения их наличия и исключения ложноположительных результатов требуется проведение ручного тестирования.  

Полная версия отчета Nikto (7788) - [NiktoReport_7788](reports/nikto/7788_nikto_report.html)

___

## 3. Сканирование с использованием Gobuster

### NetologyVulnApp.com (8050)

**Цель:**  
- веб-приложение, доступное по адресу `92.51.39.106:8050`

**Конфигурация:**  
```
gobuster dir -u http://92.51.39.106:8050 -w dirbrute.txt -t 50 -o output.html -f
```

**Результат:**  
<details>
<summary>screenshot Gobuster(8050)</summary>
 
![](screenshots/SCANNING/gobuster/gobuster_8050.png)

</details>

**Вывод:**  
В ходе анализа с использованием сканера Gobuster были выявлены несколько директорий, которые своим существованием и доступностью могут представлять угрозу для веб-приложения. Для исключения false-positive результатов необходимо провести ручную проверку обнаруженных директорий.  

Полная версия отчета Gobuster (8050) - [GobusterReport_8050](reports/gobuster/8050_gobuster_report.html)

___

### Beemer (7788)

**Цель:**  
- веб-приложение, доступное по адресу `92.51.39.106:7788`

**Конфигурация:**  
```
gobuster dir -u http://92.51.39.106:7788 -w dirbrute.txt -t 50 -o output.html -f
```

**Результат:**  
<details>
<summary>screenshot Gobuster(7788)</summary>
 
![](screenshots/SCANNING/gobuster/gobuster_7788.png)

</details>

**Вывод:**  
В ходе анализа с использованием сканера Gobuster не были выявлены скрытые и потенциально опасные директории, но вероятность их существования все равно присутствует. Необходимо провести сканирование другим инструментом, а также провести ручное тестирование.  

Полная версия отчета Gobuster (7788) - [GobusterReport_7788](reports/gobuster/7788_gobuster_report.html)

___

## 4. Сканирование с использованием FFUF

### NetologyVulnApp.com (8050)
**Цель:**  
- веб-приложение, доступное по адресу `92.51.39.106:8050`

**Конфигурация:**  
```
ffuf -w dirbrute.txt -u http://92.51.39.106:8050/FUZZ -t 50 -o output.html -of html
```

**Результат:**  
<details>
<summary>screenshot FFUF(8050)</summary>
 
![](screenshots/SCANNING/ffuf/ffuf_8050.png)

</details>

**Вывод:**  
В процессе сканирования утилитой FFUF были обнаружены несколько директорий и файлов, которые могут представлять потенциальную угрозу для безопасности веб-приложения из-за их доступности. Для исключения false-positive результатов будет проведено ручное тестирование.  

Полная версия отчета FFUF (8050) - [FFUFReport_8050](reports/ffuf/8050_ffuf_report.html)

___

### Beemer (7788)

**Цель:**  
- веб-приложение, доступное по адресу `92.51.39.106:7788`

**Конфигурация:**  
```
ffuf -w dirbrute.txt -u http://92.51.39.106:7788/FUZZ -t 50 -o output.html -of html
```

**Результат:**  
<details>
<summary>screenshot FFUF(7788)</summary>
 
![](screenshots/SCANNING/ffuf/ffuf_7788.png)

</details>

**Вывод:**  
В процессе сканирования утилитой FFUF были обнаружены несколько директорий и файлов, которые могут представлять потенциальную угрозу для безопасности веб-приложения из-за их доступности. Для исключения false-positive результатов будет проведено ручное тестирование.  

Полная версия отчета FFUF (7788) - [FFUFReport_7788](reports/ffuf/7788_ffuf_report.html)

___

## 5. Сканирование с использованием ZAP

### NetologyVulnApp.com (8050)
**Цель:**  
- веб-приложение, доступное по адресу `92.51.39.106:8050`

**Конфигурация:**  
`Active Scan + AJAX Spider`

**Результат:**  
<details>
<summary>screenshot ZAP(8050)</summary>
 
![](screenshots/SCANNING/ZAP/zap_8050.png)

</details>

**Вывод:**  
В ходе автоматического сканирования с использованием OWASP ZAP были выявлены уязвимости, которым подвержено целевое веб-приложение. Обнаруженные уязвимости варьируются по степени критичности от незначительных до критических.  

Полная версия отчета ZAP (8050) - [ZAPReport_8050](reports/zap/8050_zap_report.html)

___

### Beemer (7788)
**Цель:**  
- веб-приложение, доступное по адресу `92.51.39.106:7788`

**Конфигурация:**  
`Active Scan + AJAX Spider`

**Результат:**  
<details>
<summary>screenshot ZAP(7788)</summary>
 
![](screenshots/SCANNING/ZAP/zap_7788.png)

</details>

**Вывод:**  
В ходе автоматического сканирования с использованием OWASP ZAP были выявлены уязвимости, которым подвержено целевое веб-приложение. Обнаруженные уязвимости варьируются по степени критичности от незначительных до критических.  

Полная версия отчета ZAP (7788) - [ZAPReport_7788](reports/zap/7788_zap_report.html)

___

## Результаты сканирования веб-приложений

В ходе автоматического сканирования двух целевых веб-приложений — `NetologyVulnApp.com`  и `Beemer` — с использованием инструментов `Nmap`, `Nikto`, `Gobuster`, `FFUF` и `ZAP` были получены данные, которые послужат ориентиром для последующего ручного тестирования на проникновение.  

### 1. Основные уязвимости в веб-приложениях

#### NetologyVulnApp.com (8050)

- SQL Injection
- Cross-Site Scripting
- Cookie No Http Only Flag
- Cookie without Same Site Attribute
- Path Traversal
- Directory Browsing

#### Beemer (7788)

- Remote OS Command Injection
- SQL Injection
- Application Error Disclosure
- Cross-Site Scripting
- Cookie No HttpOnly Flag
- Cookie without SameSite Attribute
- Path Traversal
- Directory Browsing

___

### 2. Потенциально опасные директории и файлы

#### NetologyVulnApp.com (8050)
`/upload/`
`/test.php`
`/admin/`
`/admin/?/login`
`/action`

#### Beemer (7788)

- Не выявлено

___

## Перейти к следующей странице
 
Далее: Этап №3. [**TESTING**](./TESTING.md)

___
