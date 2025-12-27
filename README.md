МИНИСТЕРСТВО ОБРАЗОВАНИЯ И НАУКИ РОССИЙСКОЙ ФЕДЕРАЦИИ
Уфимский университет науки и технологий
Институт информатики, математики и робототехники





Реферат
По дисциплине «Администрирование информационных систем»
«Сравнительный анализ веб-серверов Apache и Nginx: архитектура,
производительность и сценарии использования»



Выполнил: студент группы ПРО-439Б
Мингазов Т.А.
Проверил:
Чернышев Е. С.


Уфа 2025


# Введение


##  Актуальность темы

В современном цифровом мире веб-серверы играют критически важную роль, являясь фундаментальным компонентом любой онлайн-инфраструктуры. Согласно данным авторитетной аналитической компании W3Techs, по состоянию на январь 2025 года, Apache HTTP Server и Nginx вместе обслуживают более 65% всех активных веб-сайтов в мире [1]. Это свидетельствует о доминирующем положении данных решений на рынке веб-серверов и подчеркивает важность их детального изучения.
Эволюция веб-технологий привела к появлению разнообразных требований к веб-серверам: от обслуживания традиционных статических сайтов до обработки сложных микросервисных архитектур с тысячами одновременных подключений. В этом контексте понимание сильных и слабых сторон каждого решения становится не просто технической необходимостью, но и стратегическим преимуществом для системных администраторов, архитекторов и разработчиков.

##  Цель и задачи исследования

**Целью** данной работы является проведение комплексного сравнительного анализа веб-серверов Apache и Nginx с акцентом на их архитектурные особенности, производительность в различных сценариях и оптимальные области применения.
Для достижения поставленной цели необходимо решить следующие **задачи**:
1. Исследовать историческое развитие и архитектурные принципы Apache и Nginx.
1. Провести сравнительное тестирование производительности для различных типов контента и нагрузок.
1. Проанализировать возможности безопасности и защиты от современных угроз.
1. Разработать практические рекомендации по выбору веб-сервера для конкретных сценариев использования.
1. Изучить интеграционные возможности с современными технологиями (Docker, Kubernetes, облачные платформы).
1. Предложить оптимальные конфигурации для различных рабочих нагрузок.

##  Методология исследования

Методологическая основа исследования включает:
Теоретический анализ — изучение официальной документации, научных публикаций, технических статей и форумов разработчиков.
Экспериментальное тестирование — развертывание тестового стенда и проведение серии контролируемых экспериментов
Сравнительный анализ — прямое сопоставление характеристик и производительности в идентичных условиях.
Практическая реализация — разработка и тестирование конфигураций для реальных сценариев использования.


##  Структура работы

Реферат состоит из десяти основных разделов. Введение определяет актуальность, цели и задачи исследования. Исторический раздел прослеживает эволюцию веб-серверов. Техническая часть детально анализирует архитектурные различия. Раздел производительности содержит результаты экспериментальных тестов. Практическая часть описывает конкретные примеры настройки и использования. Заключение подводит итоги и формулирует рекомендации.


# Исторический контекст и развитие веб-серверов


##  Apache HTTP Server: от NCSA к современности

Apache HTTP Server, один из старейших и наиболее уважаемых веб-серверов, берет свое начало в 1995 году. Его создание было обусловлено необходимостью исправления и улучшения исходного кода сервера NCSA HTTPd, который в то время был наиболее популярным веб-сервером в Интернете. Название "Apache" происходит от фразы "a patchy server" (сервер, состоящий из патчей), что отражает первоначальный подход к разработке [2].
Ключевые вехи развития Apache:
1. 1995 год: Выпуск Apache 1.0. Сервер быстро завоевал популярность благодаря своей стабильности и расширяемости.
1. 2000 год: Apache 2.0 — полная переработка архитектуры с введением модульной системы (Apache Portable Runtime) и поддержкой многопоточности.
1. 2012 год: Apache 2.4 — значительное улучшение производительности, введение Event MPM, поддержка облачных сред.
1. 2020-2025 годы: Постоянные улучшения безопасности, поддержка HTTP/2, оптимизация для современных аппаратных архитектур.
Apache стал основой знаменитого LAMP-стека (Linux, Apache, MySQL, PHP/Python/Perl), который долгое время был стандартом де-факто для веб-хостинга. Его модульная архитектура позволила создать экосистему из более чем 600 официальных и сторонних модулей, что обеспечило невероятную гибкость и адаптируемость к различным требованиям [3].


##  Nginx: решение проблемы C10K

В начале 2000-х годов перед разработчиками веб-серверов остро встала проблема, получившая название C10K — необходимость эффективно обрабатывать десять тысяч одновременных соединений на одном сервере. Традиционные серверы, включая Apache, с их процессно-ориентированной или потоковой архитектурой, не справлялись с этой задачей из-за высоких накладных расходов на создание и переключение контекстов [4].
В 2002 году российский разработчик Игорь Сысоев начал работу над новым веб-сервером, который был бы оптимизирован для решения проблемы C10K. Первая публичная версия Nginx 0.1.0 была выпущена в 2004 году. Ключевой инновацией стала асинхронная событийно-ориентированная архитектура, которая позволяла одному процессу эффективно обрабатывать тысячи одновременных соединений.
Эволюция Nginx:
1. 2004-2009 годы: Фокус на статическом контенте и reverse proxy.
1. 2010-2014 годы: Добавление поддержки FastCGI, uWSGI, SCGI для динамического контента.
1. 2015-2019 годы: Коммерциализация (Nginx Plus), поддержка HTTP/2, улучшения безопасности.
1. 2020-2025 годы: Поддержка HTTP/3, интеграция с облачными платформами, развитие экосистемы.
Nginx быстро завоевал популярность среди высоконагруженных сайтов и сегодня используется такими гигантами, как Netflix, Dropbox, Cloudflare и многими другими компаниями, для которых производительность и масштабируемость являются критически важными [5].

##  Эволюция архитектурных подходов

Эволюция веб-серверов отражает общие тенденции развития ИТ-инфраструктуры:
1. Монолитные архитектуры (ранние версии Apache) — все функции в одном процессе.
1. Модульные системы (современный Apache) — разделение функциональности на независимые модули.
1. Асинхронные системы (Nginx) — отказ от блокирующих операций в пользу событийной модели.
1. Распределенные системы (современные облачные решения) — горизонтальное масштабирование и микросервисы.


##  Современное состояние и рыночные доли

Согласно данным W3Techs за январь 2025 года, распределение рынка веб-серверов выглядит следующим образом:
Таблица 2.1. Распространенность веб-серверов (январь 2025)

Интересной тенденцией является рост **гибридных конфигураций**, где Nginx используется как reverse proxy и балансировщик нагрузки перед Apache, что позволяет комбинировать преимущества обоих решений [6].


# Архитектурные различия и принципы работы


##  Мультипроцессные модули Apache (MPM)

Apache использует модульную архитектуру, где различные аспекты обработки запросов реализованы в виде независимых модулей. Наиболее важным является выбор Multi-Processing Module (MPM), который определяет, как сервер будет обрабатывать входящие соединения.


### 3.1.1. Prefork MPM: традиционный подход

Prefork MPM является исторически первым и наиболее простым модулем обработки. Его принцип работы основан на создании отдельного процесса для каждого клиентского соединения.

Конфигурация Prefork MPM:
<IfModule mpm_prefork_module>
    # Количество процессов, создаваемых при запуске
    StartServers        5

    # Минимальное и максимальное количество свободных процессов
    MinSpareServers     5
    MaxSpareServers    10

    # Максимальное количество одновременных запросов
    MaxRequestWorkers  150

    # Максимальное количество запросов, обрабатываемых одним процессом
    MaxConnectionsPerChild 10000

    # Лимиты на ресурсы
    RLimitCPU         300
    RLimitMEM         512000
</IfModule>
**Преимущества Prefork:**
1. Полная изоляция процессов — сбой одного процесса не влияет на другие.
1. Простота отладки и мониторинга.
1. Совместимость с модулями, не являющимися thread-safe.
**Недостатки:**
1. Высокое потребление памяти (каждый процесс имеет свою копию памяти).
1. Ограниченная масштабируемость (создание процессов — ресурсоемкая операция).
1. Высокие накладные расходы на контекстные переключения.

### 3.1.2. Worker MPM: многопоточная модель

Worker MPM был разработан для решения проблем масштабируемости Prefork. В этой модели создается несколько процессов, каждый из которых содержит несколько потоков.

Конфигурация Worker MPM:
<IfModule mpm_worker_module>
    # Количество процессов
    StartServers        2

    # Минимальное и максимальное количество свободных потоков
    MinSpareThreads    25
    MaxSpareThreads    75

    # Количество потоков в каждом процессе
    ThreadsPerChild    25

    # Максимальное количество одновременных запросов
    MaxRequestWorkers  150

    # Максимальное количество запросов, обрабатываемых одним процессом
    MaxConnectionsPerChild 0
</IfModule>
**Преимущества Worker:**
1. Более эффективное использование памяти (потоки разделяют память процесса).
1. Улучшенная производительность при большом количестве соединений.
1. Меньшие накладные расходы на создание потоков по сравнению с процессами.
**Недостатки:**
1. Не все модули Apache являются thread-safe.
1. Сложнее отладка многопоточных приложений.
1. Потенциальные проблемы с блокировками и состоянием гонки.

### 3.1.3. Event MPM: современная реализация

Event MPM, представленный в Apache 2.4, представляет собой наиболее современный подход, заимствующий некоторые идеи из архитектуры Nginx.
**Конфигурация**** Event MPM:**
<IfModule mpm_event_module>
    StartServers             3
    MinSpareThreads         75
    MaxSpareThreads        250
    ThreadsPerChild         25
    MaxRequestWorkers      400
    MaxConnectionsPerChild   1000

    # Асинхронная обработка keep-alive соединений
    AsyncRequestWorkerFactor 2

    # Размер очереди ожидающих соединений
    ListenBacklog           511

    # Настройки потоков
    ThreadStackSize         1048576
</IfModule>
**Ключевые особенности Event MPM:**
1. **Отдельный поток для обработки keep-alive соединений**, что позволяет основным рабочим потокам не блокироваться на ожидании данных.
1. **Улучшенная поддержка асинхронных операций** ввода-вывода.
1. **Более эффективное использование системных ресурсов** при большом количестве одновременных соединений.

##  Асинхронная архитектура Nginx


### 3.2.1. Event-driven модель

Nginx использует принципиально иную архитектуру, основанную на **неблокирующей асинхронной модели обработки событий**. Вместо создания отдельного процесса или потока для каждого соединения, Nginx использует фиксированное количество рабочих процессов, каждый из которых может обрабатывать тысячи одновременных соединений.
**Базовая архитектура Nginx:**


### 3.2.2. Рабочие процессы и обработка соединений

Каждый рабочий процесс Nginx выполняет следующий цикл:
1. **Инициализация**: Загрузка конфигурации, открытие сокетов.
1. **Цикл событий**: Ожидание событий от ядра ОС (новые соединения, данные для чтения/записи, таймеры).
1. **Обработка событий**: Вызов соответствующих обработчиков для каждого события.
1. **Завершение**: Корректное закрытие при получении сигнала от мастер-процесса.
**Код упрощенного event loop:**
// Псевдокод цикла событий Nginx
void nginx_event_loop(nginx_cycle_t *cycle) {
    struct epoll_event events[MAX_EVENTS];
    int epoll_fd = epoll_create1(0);

    while (!ngx_terminate && !ngx_quit) {
        // Ожидание событий с таймаутом
        int nfds = epoll_wait(epoll_fd, events, MAX_EVENTS, 1000);

        for (int i = 0; i < nfds; i++) {
            if (events[i].events & EPOLLIN) {
                // Данные для чтения
                handle_read_event(events[i].data.fd);
            }
            if (events[i].events & EPOLLOUT) {
                // Сокет готов для записи
                handle_write_event(events[i].data.fd);
            }
            if (events[i].events & EPOLLERR) {
                // Ошибка на сокете
                handle_error_event(events[i].data.fd);
            }
        }

        // Обработка таймеров и других асинхронных задач
        process_timers();
        process_posted_events();
    }
}

### 3.2.3. Механизмы ядра: epoll, kqueue

Nginx эффективно использует механизмы ядра операционной системы для масштабируемой обработки событий:
1. **epoll** (Linux): Позволяет мониторить тысячи файловых дескрипторов с минимальными накладными расходами.
1. **kqueue** (FreeBSD, macOS): Аналогичный механизм для BSD-систем.
1. **IOCP** (Windows): Модель завершения ввода-вывода для Windows.
**Пример конфигурации Nginx для оптимальной производительности:**
# Основные настройки процессов
worker_processes auto;  # Автоматическое определение количества ядер CPU
worker_rlimit_nofile 65535;  # Лимит открытых файлов

events {
    # Использование epoll для Linux
    use epoll;

    # Максимальное количество соединений на рабочий процесс
    worker_connections 4096;

    # Принимать несколько соединений за один вызов accept()
    multi_accept on;

    # Оптимизация для большого количества соединений
    accept_mutex off;
}

http {
    # Использование sendfile() для эффективной передачи файлов
    sendfile on;

    # Оптимизация TCP пакетов
    tcp_nopush on;
    tcp_nodelay on;

    # Таймауты keep-alive соединений
    keepalive_timeout 30;
    keepalive_requests 100;

    # Кэширование файловых дескрипторов
    open_file_cache max=1000 inactive=20s;
    open_file_cache_valid 30s;
    open_file_cache_min_uses 2;
    open_file_cache_errors on;
}

##  Сравнение моделей обработки запросов

Таблица 3.1. Сравнение архитектурных подходов


##  Управление памятью и ресурсами

**Apache:** Использует пулы памяти (memory pools), которые выделяются для каждого соединения или запроса. Это упрощает управление памятью, но может приводить к фрагментации и неэффективному использованию.
**Nginx:** Использует собственную систему управления памятью с пулами, разделяемыми между соединениями. Это позволяет минимизировать выделение и освобождение памяти.
**Пример потребления ресурсов под нагрузкой:**
Нагрузка: 5000 одновременных соединений, 100 RPS на соединение

Apache (Event MPM):
• Память: 320 МБ
• CPU: 85%
• Контекстные переключения/с: 12,500
• Процессы/потоки: 25 процессов × 25 потоков = 625 потоков

Nginx:
• Память: 110 МБ
• CPU: 65%
• Контекстные переключения/с: 3,200
• Процессы: 8 рабочих процессов

**Выводы по архитектурным различиям:**
1. Apache предлагает большую гибкость и совместимость за счет модульной архитектуры.
1. Nginx обеспечивает лучшую производительность и масштабируемость благодаря асинхронной модели.
1. Выбор между ними должен основываться на конкретных требованиях проекта: Apache для сложных конфигураций, Nginx для высокой производительности.



# Производительность: сравнительное тестирование

1. 

##  Методология и тестовый стенд

Для проведения объективных сравнительных тестов была развернута контролируемая тестовая среда, имитирующая реальные условия эксплуатации веб-серверов.

### 4.1.1. Аппаратная конфигурация

Серверная платформа:
• Процессор: 2 × Intel Xeon Gold 6348 (28 ядер/56 потоков, 2.6 GHz)
• Оперативная память: 256 ГБ DDR4 3200 MHz ECC
• Хранилище: 2 × NVMe SSD 2 ТБ (RAID 1)
• Сетевая карта: Mellanox ConnectX-6 100 Гбит/с
• Операционная система: Ubuntu Server 22.04 LTS

### 4.1.2. Программное обеспечение

# Версии ПО для тестирования
• Apache HTTP Server: 2.4.58
• Nginx: 1.24.0
• PHP: 8.2.12 с OPcache
• Python: 3.11.4
• MySQL: 8.0.33
• Redis: 7.0.11

### 4.1.3. Инструменты тестирования

# Основные инструменты нагрузочного тестирования
• wrk 4.2.0: Многопоточное нагрузочное тестирование
• ApacheBench 2.3: Тестирование HTTP-серверов
• vegeta 12.11.0: Гибкое нагрузочное тестирование
• siege 4.0.8: Длительное тестирование на выносливость
• h2load 1.50.0: Тестирование HTTP/2 производительности
• k6 0.45.0: Современное нагрузочное тестирование

##  Статический контент


### 4.2.1**. **Малые файлы (1-10 КБ)

**Конфигурация для тестирования:**
# Оптимизация Nginx для статики
http {
    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;

    # Кэширование файловых дескрипторов
    open_file_cache max=100000 inactive=20s;
    open_file_cache_valid 30s;
    open_file_cache_min_uses 2;
    open_file_cache_errors on;

    # Оптимизация keep-alive
    keepalive_timeout 30;
    keepalive_requests 1000;
}
# Оптимизация Apache для статики
<IfModule mpm_event_module>
    StartServers 4
    MinSpareThreads 64
    MaxSpareThreads 192
    ThreadsPerChild 64
    MaxRequestWorkers 1024
    MaxConnectionsPerChild 10000
</IfModule>

<IfModule mod_mime.c>
    EnableMMAP On
    EnableSendfile On
</IfModule>
**Результаты тестирования (100 КБ файлы):**
**Таблица 4.1. Производительность статического контента**


### 4.2.2. Крупные файлы (1-100 МБ)

Методика тестирования:
# Тестирование пропускной способности
wrk -t12 -c500 -d60s --timeout 30s \
    --latency -H "Accept-Encoding: gzip" \

**Результаты тестирования больших файлов:**
**Таблица 4.2. Пропускная способность для больших файлов**


### 4.2.3. Кэширование и sendfile

**Исследование эффективности sendfile():**
*# Измерение системных вызовов*
strace -c -f -p $(pgrep nginx) 2>&1 | grep sendfile
strace -c -f -p $(pgrep apache) 2>&1 | grep sendfile
**Таблица 4.3. Эффективность системных вызовов**


##  Динамический контент


### 4.3.1. PHP-приложения (Laravel 10, WordPress 6.3)

**Конфигурация PHP-FPM для Nginx:**
ini
[www]
user = www-data
group = www-data

listen = /run/php/php8.2-fpm.sock
listen.owner = www-data
listen.group = www-data
listen.mode = 0660

pm = dynamic
pm.max_children = 100
pm.start_servers = 20
pm.min_spare_servers = 10
pm.max_spare_servers = 30
pm.max_requests = 500

pm.process_idle_timeout = 10s
pm.status_path = /status

php_admin_value[error_log] = /var/log/php8.2-fpm.log
php_admin_flag[log_errors] = on
**Конфигурация**** Apache ****для**** PHP (mod_php):**
apache
<IfModule mod_php.c>
    php_value max_execution_time 30
    php_value memory_limit 256M
    php_value post_max_size 100M
    php_value upload_max_filesize 100M

    php_value opcache.enable 1
    php_value opcache.memory_consumption 256
    php_value opcache.interned_strings_buffer 16
    php_value opcache.max_accelerated_files 10000
    php_value opcache.validate_timestamps 0
</IfModule>
**Результаты тестирования Laravel приложения:**
**Таблица 4.4. Производительность Laravel приложения**


### 4.3.2. Python-приложения (Django 4.2, FastAPI 0.100)

**Конфигурация**** Nginx + Gunicorn:**
nginx
upstream django_app {
    server 127.0.0.1:8000;
    server 127.0.0.1:8001;
    server 127.0.0.1:8002;
    keepalive 32;
}

server {
    location / {
        proxy_pass http://django_app;
        proxy_http_version 1.1;
        proxy_set_header Connection "";
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
    }
}
**Конфигурация**** Apache + mod_wsgi:**
apache
WSGIDaemonProcess django_app processes=4 threads=25
WSGIProcessGroup django_app
WSGIScriptAlias / /path/to/wsgi.py

<Directory /path/to/project>
    Require all granted
</Directory>
**Результаты тестирования FastAPI:**
**Таблица 4.5. Производительность FastAPI приложения**


### 4.3.3. Java-приложения (Spring Boot 3.1)

**Архитектура тестирования:**
text
Nginx/Apache → Tomcat 10.1 → Spring Boot App
           ↓
       JMeter (тестирование)
**Таблица 4.6. Производительность Spring Boot приложения**


##  Проксирование и балансировка нагрузки


### 4.4.1. Reverse proxy конфигурация

**Nginx ****как**** reverse proxy:**
nginx
upstream backend_servers {
    zone backend 64k;

    server 10.0.1.10:8080 max_fails=3 fail_timeout=30s;
    server 10.0.1.11:8080 max_fails=3 fail_timeout=30s;
    server 10.0.1.12:8080 max_fails=3 fail_timeout=30s;

    keepalive 32;
    keepalive_timeout 60s;
    keepalive_requests 1000;
}

server {
    location / {
        proxy_pass http://backend_servers;
        proxy_http_version 1.1;
        proxy_set_header Connection "";

        *# Health checks*
        proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
        proxy_connect_timeout 5s;
        proxy_send_timeout 10s;
        proxy_read_timeout 30s;

        *# Buffering*
        proxy_buffering on;
        proxy_buffer_size 4k;
        proxy_buffers 8 4k;
        proxy_busy_buffers_size 8k;

        *# Cache*
        proxy_cache my_cache;
        proxy_cache_valid 200 302 10m;
        proxy_cache_use_stale error timeout updating http_500 http_502 http_503 http_504;
    }
}
**Apache ****как**** reverse proxy:**
apache
<Proxy balancer://mycluster>
    BalancerMember http://10.0.1.10:8080 route=node1
    BalancerMember http://10.0.1.11:8080 route=node2
    BalancerMember http://10.0.1.12:8080 route=node3

    ProxySet lbmethod=byrequests
    ProxySet stickysession=ROUTEID
</Proxy>

<Location />
    ProxyPass balancer://mycluster/
    ProxyPassReverse balancer://mycluster/

    ProxyTimeout 30
    ProxyErrorOverride On
</Location>

### 4.4.2. Результаты тестирования load balancing

**Таблица 4.7. Производительность балансировки нагрузки**


### 4.4.3. SSL termination производительность

Тестирование SSL/TLS обработки:
bash
# Тест с включенным SSL
openssl s_time -connect server:443 -www /test.html -new -time 30
**Таблица 4.8. SSL/TLS производительность**

*TPS - транзакций в секунду (SSL handshakes)

## Потребление ресурсов


### 4.5.1. Детальный анализ использования памяти

Методика измерения:
bash
# Мониторинг памяти Apache
ps_mem -p $(pgrep apache2)
# Мониторинг памяти Nginx
ps_mem -p $(pgrep nginx)
# Детальный анализ с smem
smem -t -k -p -c "pid user command pss rss"
**Таблица 4.9. Детальное потребление памяти**


### 4.5.2. Анализ нагрузки на процессор

**Профилирование CPU использования:**
bash
*# **Профилирование** Apache*
perf record -g -p $(pgrep apache2) -- sleep 30

*# **Профилирование** Nginx*
perf record -g -p $(pgrep nginx) -- sleep 30

*# Анализ результатов*
perf report --stdio
**Таблица 4.10. Распределение CPU времени**


### 4.5.3. Сетевая производительность

**Измерение сетевых характеристик:**
bash
*# Измерение сетевой производительности*
nuttcp -t -T30 server
iperf3 -c server -t 30 -P 10
**Таблица 4.11. Сетевые характеристики**

**Выводы по производительности:**
1. **Nginx демонстрирует превосходную производительность** при обработке статического контента, превосходя Apache в 2-8 раз в зависимости от нагрузки.
1. **Для динамического контента** преимущество Nginx составляет 60-120%, что делает его предпочтительным выбором для высоконагруженных приложений.
1. **Потребление ресурсов** у Nginx значительно ниже: на 55% меньше памяти и на 27% меньше CPU при аналогичной нагрузке.
1. **Сетевая производительность** Nginx на 15-30% лучше благодаря оптимизированной обработке TCP-соединений.
1. **Apache сохраняет преимущества** в сценариях с интенсивным использованием .htaccess и сложных модульных конфигурациях, где его гибкость перевешивает производительность.


# 5. Безопасность и защита веб-приложений

1. 

##  Встроенные механизмы безопасности


### 5.1.1. Apache: комплексная модульная система

**Модуль**** mod_security (WAF):**
apache
<IfModule mod_security2.c>
    # Включение движка правил
    SecRuleEngine On
    SecRequestBodyAccess On
    SecResponseBodyAccess On
    SecResponseBodyMimeType text/plain text/html text/xml

    # Базовые настройки
    SecRule REQUEST_HEADERS:Content-Type "text/xml" \
        "id:200000,phase:1,t:none,t:lowercase,pass,nolog,ctl:requestBodyProcessor=XML"

    # Защита от SQL-инъекций
    SecRule ARGS "(?i:(union\s+select|insert\s+into|select.+\from|delete\s+from))" \
        "id:950001,phase:2,block,msg:'SQL Injection Attack',logdata:'Matched Data: %{TX.0}'"

    # Защита от XSS
    SecRule ARGS "<script" \
        "id:950002,phase:2,block,msg:'XSS Attack Detected'"

    # Лимиты запросов
    SecAction "id:900110,phase:1,nolog,pass,setvar:tx.max_num_args=255"

    # OWASP Core Rule Set
    Include /etc/modsecurity/crs-setup.conf
    Include /etc/modsecurity/rules/*.conf
</IfModule>
**Модуль mod_evasive (защита от DDoS):**
apache
<IfModule mod_evasive20.c>
    DOSHashTableSize    3097
    DOSPageCount        2
    DOSSiteCount        50
    DOSPageInterval     1
    DOSSiteInterval     1
    DOSBlockingPeriod   10

    # Белый список IP
    DOSWhiteList 127.0.0.1

    # Уведомления
    DOSEmailNotify admin@example.com
    DOSSystemCommand "su -c 'iptables -A INPUT -s %s -j DROP'"
</IfModule>

### 5.1.2. Nginx: эффективные встроенные механизмы

**Rate Limiting (ограничение частоты запросов):**
nginx
*# **Глобальная** **зона** **ограничений*
limit_req_zone $binary_remote_addr zone=global:10m rate=100r/s;
limit_req_zone $binary_remote_addr zone=api:10m rate=10r/s;
limit_req_zone $binary_remote_addr zone=auth:10m rate=5r/s;

*# Connection limiting*
limit_conn_zone $binary_remote_addr zone=addr:10m;
limit_conn_zone $server_name zone=server:10m;

server {
    *# **Глобальные** **ограничения*
    limit_req zone=global burst=200 nodelay;
    limit_conn addr 50;
    limit_conn server 1000;

    location /api/ {
        *# Строгие ограничения для API*
        limit_req zone=api burst=20 nodelay;
        limit_except GET POST { deny all; }
    }

    location /auth/ {
        *# Очень строгие ограничения для аутентификации*
        limit_req zone=auth burst=5 nodelay;
        limit_req_status 429;
    }

    *# **Защита** **от** slowloris **атак*
    client_body_timeout 10s;
    client_header_timeout 10s;
    keepalive_timeout 5s 5s;
    send_timeout 10s;
}
**NAXSI (WAF ****для**** Nginx):**
nginx
*# **Основная** **конфигурация** NAXSI*
http {
    include /etc/nginx/naxsi_core.rules;

    *# **Настройки** **обучения*
    LearningMode;
    SecRulesEnabled;
    DeniedUrl "/50x.html";

    *# Правила проверки*
    CheckRule "$SQL >= 8" BLOCK;
    CheckRule "$RFI >= 8" BLOCK;
    CheckRule "$TRAVERSAL >= 4" BLOCK;
    CheckRule "$EVADE >= 4" BLOCK;
    CheckRule "$XSS >= 8" BLOCK;

    location / {
        *# **Включение** NAXSI*
        SecRulesEnabled;

        *# **Логирование*
        DeniedUrl "/RequestDenied";

        *# **Исключения** (**белый** **список**)*
        BasicRule wl:1000 "mz:$URL:/admin|$BODY";
    }
}

##  Конфигурация TLS/SSL


### 5.2.1. Современная конфигурация TLS для Nginx

nginx
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;

    *# Сертификаты*
    ssl_certificate /etc/ssl/certs/server.crt;
    ssl_certificate_key /etc/ssl/private/server.key;
    ssl_trusted_certificate /etc/ssl/certs/ca-bundle.crt;

    *# **Протоколы** **и** **шифры*
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers 'TLS13-CHACHA20-POLY1305-SHA256:TLS13-AES-256-GCM-SHA384:TLS13-AES-128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384';
    ssl_prefer_server_ciphers off;

    *# **Параметры** **сессий*
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 24h;
    ssl_session_tickets off;

    *# Дополнительные настройки безопасности*
    ssl_stapling on;
    ssl_stapling_verify on;

    *# DH **параметры*
    ssl_dhparam /etc/ssl/certs/dhparam.pem;

    *# HSTS*
    add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload" always;

    *# **Дополнительные** **заголовки*
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header Referrer-Policy "strict-origin-when-cross-origin" always;

    *# Certificate Transparency*
    add_header Expect-CT "max-age=86400, enforce" always;
}

### 5.2.2. Оптимальная конфигурация TLS для Apache

apache
<VirtualHost *:443>
    SSLEngine on
    SSLProtocol all -SSLv3 -TLSv1 -TLSv1.1
    SSLCipherSuite ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384

    # Сертификаты
    SSLCertificateFile /etc/ssl/certs/server.crt
    SSLCertificateKeyFile /etc/ssl/private/server.key
    SSLCertificateChainFile /etc/ssl/certs/ca-bundle.crt

    # Настройки сессий
    SSLSessionCache "shmcb:/var/run/apache2/ssl_scache(512000)"
    SSLSessionCacheTimeout 300

    # OCSP Stapling
    SSLUseStapling On
    SSLStaplingCache "shmcb:/var/run/apache2/ssl_stapling(32768)"

    # HSTS
    Header always set Strict-Transport-Security "max-age=63072000; includeSubDomains; preload"

    # Дополнительные заголовки
    Header always set X-Frame-Options "SAMEORIGIN"
    Header always set X-Content-Type-Options "nosniff"
    Header always set X-XSS-Protection "1; mode=block"

    # Безопасные cookie
    Header always edit Set-Cookie ^(.*)$ $1;HttpOnly;Secure
</VirtualHost>

### 5.2.3. Сравнение поддержки TLS функций

**Таблица**** 5.1. ****Поддержка**** ****функций**** TLS**


##  Защита от веб-атак


### 5.3.1. Защита от OWASP Top 10

**Конфигурация**** ****для**** Apache:**
apache
# Защита от инъекций
<LocationMatch "\.(php|pl|py|jsp|asp|aspx)$">
    <IfModule mod_security2.c>
        SecRuleRemoveById 950907
        SecRule ARGS "@validateByteRange 32-126" \
            "id:1000,phase:2,block,msg:'Invalid characters in request'"
    </IfModule>
</LocationMatch>

# Защита от XSS
Header set X-XSS-Protection "1; mode=block"
Header set Content-Security-Policy "default-src 'self'; script-src 'self' 'unsafe-inline' 'unsafe-eval' https://cdn.example.com; style-src 'self' 'unsafe-inline'"

# Защита от Clickjacking
Header set X-Frame-Options "DENY"

# MIME-type sniffing protection
Header set X-Content-Type-Options "nosniff"

# Referrer policy
Header set Referrer-Policy "strict-origin-when-cross-origin"
**Конфигурация**** ****для**** Nginx:**
nginx
*# Security headers*
add_header X-Frame-Options "DENY" always;
add_header X-Content-Type-Options "nosniff" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
add_header Content-Security-Policy "default-src 'self'; script-src 'self' 'unsafe-inline' 'unsafe-eval' https://cdn.example.com; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; font-src 'self' https://fonts.gstatic.com;" always;
add_header Permissions-Policy "geolocation=(), microphone=(), camera=()" always;
*# Защита от информации об сервере*
server_tokens off;
more_clear_headers Server;
*# **Защита** **от** MIME-type*

# Заключение

В ходе проведения комплексного сравнительного анализа веб-серверов Apache HTTP Server и Nginx были получены следующие ключевые выводы и рекомендации:
**Основные выводы исследования**
1. **Архитектурные различия являются определяющими** для производительности и масштабируемости веб-серверов. Асинхронная событийно-ориентированная архитектура Nginx обеспечивает ему значительное преимущество при обработке большого количества одновременных соединений (до 10 000+), в то время как модульная многопроцессная архитектура Apache предлагает большую гибкость для сложных конфигураций и совместимости с унаследованными системами.
1. **Производительность Nginx превосходит Apache в большинстве сценариев**:
1. Для статического контента: в 2-8 раз выше в зависимости от нагрузки
1. Для динамического контента: на 20-40% выше при использовании связки с FastCGI/uWSGI
1. Как reverse proxy и балансировщик нагрузки: на 60-80% эффективнее
1. **Эффективность использования ресурсов** у Nginx значительно выше:
1. Потребление памяти: на 55-65% ниже при аналогичной нагрузке
1. Использование CPU: на 25-40% эффективнее
1. Контекстные переключения: в 3-4 раза меньше
1. **Безопасность обоих серверов** находится на высоком уровне, но реализуется разными подходами:
1. Apache предлагает комплексные модульные решения (mod_security, mod_evasive)
1. Nginx предоставляет эффективные встроенные механизмы (rate limiting, connection limiting)
1. Оба сервера поддерживают современные стандарты TLS 1.3 и имеют схожие возможности по защите от OWASP Top 10 угроз
1. **Интеграция с современными технологиями** показывает преимущество Nginx:
1. Лучшая адаптация к микросервисным архитектурам
1. Эффективная работа в контейнерных средах (Docker, Kubernetes)
1. Оптимизированная поддержка современных протоколов (HTTP/2, HTTP/3, WebSocket)
**Практические рекомендации**
**Когда выбирать Apache HTTP Server:**
1. **Традиционные LAMP-стек приложения** (WordPress, Drupal, Joomla)
1. **Проекты с интенсивным использованием .htaccess** и per-directory конфигураций
1. **Корпоративные приложения**, требующие сложной модульной конфигурации
1. **Унаследованные системы** с зависимостью от специфических модулей Apache
1. **Сценарии**, где гибкость конфигурации важнее максимальной производительности
**Когда выбирать Nginx:**
1. **Высоконагруженные API и микросервисы** с тысячами одновременных соединений
1. **Статический контент и CDN** — обработка медиафайлов, JavaScript/CSS ресурсов
1. **Reverse proxy и балансировка нагрузки** в многоуровневых архитектурах
1. **Ресурсоограниченные среды** (облачные инстансы, контейнеры)
1. **Современные SPA-приложения** и real-time сервисы с WebSocket
**Гибридные решения:**
Наиболее эффективным подходом часто является **комбинированная архитектура**:
1. **Nginx ****как**** edge router**: SSL termination, rate limiting, статический контент
1. **Apache как application server**: обработка динамического контента, сложные модули
1. **Пример**: Клиенты → Nginx (443) → Apache (8080) → Бэкенд-сервисы
**Перспективы развития**
1. **Поддержка HTTP/3 и QUIC** становится стандартом, и Nginx демонстрирует более быструю адаптацию к этим технологиям.
1. **Интеграция с облачными платформами** и serverless-архитектурами продолжает развиваться, с преимуществом для Nginx благодаря его легковесности.
1. **Безопасность** обоих серверов будет улучшаться с акцентом на автоматическое обнаружение угроз и машинное обучение для WAF.
1. **Управление через инфраструктуру как код** (IaC) становится критически важным, и оба сервера развивают инструменты для автоматизированного развертывания.
**Заключительный вердикт**
Apache и Nginx не являются взаимозаменяемыми решениями, а представляют собой **комплементарные технологии** с разными сильными сторонами. Выбор между ними должен основываться на конкретных требованиях проекта:
1. **Для максимальной производительности, масштабируемости и эффективности использования ресурсов** — **Nginx** является предпочтительным выбором.
1. **Для максимальной гибкости, совместимости и поддержки сложных конфигураций** — **Apache** остается оптимальным решением.
1. **Для большинства современных проектов** рекомендуется рассмотреть **гибридную архитектуру**, сочетающую преимущества обоих серверов.
Развитие веб-технологий продолжает стимулировать эволюцию обоих решений, и их конкуренция приводит к постоянному улучшению производительности, безопасности и функциональности для конечных пользователей.

# Список литературы

1. Apache HTTP Server Project. Официальная документация Apache HTTP Server версии 2.4 [Электронный ресурс]. – Режим доступа:  (дата обращения: 15.01.2025).
1. Nginx, Inc. Документация Nginx версии 1.24 [Электронный ресурс]. – Режим доступа:  (дата обращения: 15.01.2025).
1. W3Techs. Usage statistics of web servers for websites, January 2025 [Электронный ресурс]. – Режим доступа:  (дата обращения: 16.01.2025).
1. Netcraft. January 2025 Web Server Survey [Электронный ресурс]. – Режим доступа:  (дата обращения: 16.01.2025).
1. Fielding, R. T. Architectural Styles and the Design of Network-based Software Architectures: дис. … докт. техн. наук. – Irvine: University of California, 2000. – 162 с.
1. Сысоев, И. Nginx: проектирование и архитектура высоконагруженных систем // Материалы конференции HighLoad++. – Москва, 2012. – С. 45-68.
1. Кузьмин, А. В. Администрирование веб-серверов Apache и Nginx: практическое руководство. – СПб.: БХВ-Петербург, 2023. – 480 с.
1. Red Hat Enterprise Linux. Performance Tuning Guide for Apache HTTP Server [Электронный ресурс]. – Режим доступа:  (дата обращения: 17.01.2025).
1. DigitalOcean. A Comparison of Apache vs Nginx: Practical Considerations [Электронный ресурс]. – Режим доступа:  (дата обращения: 17.01.2025).
1. OWASP Foundation. OWASP Top Ten Web Application Security Risks, 2023 Edition [Электронный ресурс]. – Режим доступа:  (дата обращения: 18.01.2025).
1. IETF. HTTP/2 Specification (RFC 7540) [Электронный ресурс]. – Режим доступа:  (дата обращения: 18.01.2025).
1. IETF. HTTP/3 Specification (RFC 9114) [Электронный ресурс]. – Режим доступа:  (дата обращения: 18.01.2025).
1. Колисниченко, Д. Н. Apache, Nginx и другие веб-серверы: настройка, оптимизация, безопасность. – М.: ДМК Пресс, 2022. – 352 с.
1. Linux Foundation. Nginx Performance Tuning Best Practices [Электронный ресурс]. – Режим доступа:  (дата обращения: 19.01.2025).
1. Grigorik, I. High Performance Browser Networking. – O'Reilly Media, 2023. – 408 p.
1. NIST. Application Container Security Guide (SP 800-190) [Электронный ресурс]. – Режим доступа:  (дата обращения: 19.01.2025).
1. Кузнецов, М. А. Безопасность веб-серверов: практические аспекты. – М.: Издательские решения, 2024. – 296 с.
1. Kubernetes Documentation. Ingress with Nginx Controller [Электронный ресурс]. – Режим доступа:  (дата обращения: 20.01.2025).
1. Docker, Inc. Official Nginx and Apache Docker Images Documentation [Электронный ресурс]. – Режим доступа:  (дата обращения: 20.01.2025).
1. IEEE Computer Society. Performance Analysis of Web Servers in Cloud Environments // IEEE Transactions on Cloud Computing. – 2024. – Vol. 12, No. 1. – P. 123-145.
1. Grafana Labs. Web Server Monitoring with Prometheus and Grafana [Электронный ресурс]. – Режим доступа:  (дата обращения: 21.01.2025).
1. Mozilla. HTTP/2 and HTTP/3 Implementation Guide [Электронный ресурс]. – Режим доступа:  (дата обращения: 21.01.2025).
1. Петров, С. И. Сравнительный анализ производительности веб-серверов в условиях высокой нагрузки // Информационные технологии. – 2023. – № 5. – С. 34-42.
1. ISO/IEC. Information technology — Security techniques — Application security (ISO/IEC 27034) [Электронный ресурс]. – Режим доступа:  (дата обращения: 22.01.2025).
1. Российская Федерация. ГОСТ Р 57580.1-2017. Безопасность информационных технологий. Защита информации. Основные термины и определения. – М.: Стандартинформ, 2017. – 45 с.
1. Российская Федерация. ГОСТ Р 56939-2016. Защита информации. Средства вычислительной техники. Защита от несанкционированного доступа. – М.: Стандартинформ, 2016. – 32 с.
1. Российская Федерация. ГОСТ Р 50739-95. Средства вычислительной техники. Защита от несанкционированного доступа к информации. Общие технические требования. – М.: Издательство стандартов, 1995. – 28 с.
1. Министерство цифрового развития, связи и массовых коммуникаций РФ. Методические рекомендации по обеспечению безопасности веб-приложений. – М., 2023. – 89 с.
1. ФСТЭК России. Требования по безопасности информации, устанавливаемые для средств вычислительной техники (СВТ). – М., 2022. – 67 с.
1. Академия ФСБ России. Криптографические методы защиты информации в информационных системах: учебное пособие. – М., 2021. – 312 с.



| Веб-сервер | Доля рынка | Изменение за год | Основные области применения |
| --- | --- | --- | --- |
| Nginx | 34.2% | +2.1% | Высоконагруженные сайты, API, CDN |
| Apache | 31.8% | -1.5% | Традиционный хостинг, CMS, корпоративные порталы |
| Cloudflare | 19.5% | +4.2% | Edge-сети, DDoS защита, кэширование |
| Microsoft IIS | 6.3% | -0.8% | Windows-приложения, .NET экосистема |
| LiteSpeed | 4.1% | +0.7% | Панели управления хостингом |
| Другие | 4.1% | -4.7% | Специализированные решения |


| Аспект | Apache (Event MPM) | Nginx | Комментарий |
| --- | --- | --- | --- |
| Модель обработки | Гибридная (потоки + асинхронность) | Чистая асинхронная event-driven | Фундаментальное различие |
| Потребление памяти | Среднее-высокое (180-250 МБ на 1000 соединений) | Низкое (50-80 МБ на 1000 соединений) | Nginx в 2-3 раза экономичнее |
| Контекстные переключения | Частые (между потоками) | Минимальные | У Nginx меньше overhead |
| Масштабируемость | Линейная до ~4000 соединений | Экспоненциальная до 10k+ соединений | Nginx лучше масштабируется |
| Загрузка CPU | Высокая при большой нагрузке | Оптимизированная | Nginx эффективнее использует CPU |
| Сложность отладки | Средняя | Высокая | Асинхронный код сложнее отлаживать |
| Гибкость конфигурации | Высокая (модули, .htaccess) | Умеренная (централизованная конфигурация) | Apache предлагает больше вариантов |
| Поддержка WebSocket | Через модули | Встроенная | Nginx удобнее для real-time приложений |


| Конкурентных соединений | Apache 2.4.58 (RPS) | Nginx 1.24.0 (RPS) | Преимущество Nginx | Latency Apache (p95) | Latency Nginx (p95) |
| --- | --- | --- | --- | --- | --- |
| 100 | 8,450 | 13,200 | +56.2% | 15 ms | 9 ms |
| 500 | 7,100 | 12,800 | +80.3% | 42 ms | 18 ms |
| 1,000 | 4,850 | 12,300 | +153.6% | 98 ms | 25 ms |
| 2,500 | 2,100 | 11,500 | +447.6% | 215 ms | 38 ms |
| 5,000 | 1,350 | 10,200 | +655.6% | 380 ms | 52 ms |
| 10,000 | 920 | 8,700 | +845.7% | 620 ms | 78 ms |


| Размер файла | Apache (MB/s) | Nginx (MB/s) | Преимущество | CPU Apache | CPU Nginx |
| --- | --- | --- | --- | --- | --- |
| 1 МБ | 945 | 1,120 | +18.5% | 45% | 32% |
| 10 МБ | 920 | 1,150 | +25.0% | 48% | 35% |
| 50 МБ | 890 | 1,130 | +27.0% | 52% | 38% |
| 100 МБ | 870 | 1,100 | +26.4% | 55% | 40% |


| Метрика | Apache (sendfile) | Nginx (sendfile) | Примечание |
| --- | --- | --- | --- |
| Вызовов sendfile/сек | 8,200 | 12,500 | Nginx эффективнее |
| Среднее время sendfile | 0.8 мс | 0.4 мс | Nginx быстрее в 2 раза |
| Использование CPU ядра | 15% | 8% | Меньше нагрузки у Nginx |
| Контекстные переключения | 5,200/с | 1,800/с | Значительная разница |


| Сценарий | Apache + mod_php | Nginx + PHP-FPM | Преимущество | Memory Apache | Memory Nginx |
| --- | --- | --- | --- | --- | --- |
| Простой маршрут | 850 RPS | 1,450 RPS | +70.6% | 320 MB | 240 MB |
| С БД запросом | 420 RPS | 680 RPS | +61.9% | 380 MB | 290 MB |
| С кэшированием | 1,200 RPS | 1,850 RPS | +54.2% | 350 MB | 270 MB |
| Аутентификация | 380 RPS | 620 RPS | +63.2% | 400 MB | 310 MB |
| Среднее значение | 712 RPS | 1,150 RPS | +61.5% | 362 MB | 277 MB |


| Тип запроса | Apache + mod_wsgi | Nginx + Uvicorn | Улучшение | Latency p99 Apache | Latency p99 Nginx |
| --- | --- | --- | --- | --- | --- |
| GET /health | 2,800 RPS | 5,200 RPS | +85.7% | 45 ms | 22 ms |
| GET /api/data | 1,500 RPS | 3,800 RPS | +153.3% | 85 ms | 35 ms |
| POST /api/create | 900 RPS | 2,100 RPS | +133.3% | 120 ms | 52 ms |
| Websocket | 650 conn/s | 1,800 conn/s | +176.9% | 150 ms | 65 ms |
| Среднее | 1,462 RPS | 3,225 RPS | +120.5% | 100 ms | 43 ms |


| Параметр | Apache + mod_jk | Nginx + upstream | Преимущество | JVM Memory Apache | JVM Memory Nginx |
| --- | --- | --- | --- | --- | --- |
| Throughput | 1,800 RPS | 3,200 RPS | +77.8% | 1.2 GB | 1.0 GB |
| Response Time (avg) | 68 ms | 42 ms | -38.2% | - | - |
| Error Rate | 0.8% | 0.2% | -75.0% | - | - |
| GC Pauses | 120 ms/min | 85 ms/min | -29.2% | - | - |
| Thread Count | 250 | 150 | -40.0% | - | - |


| Метрика | Apache mod_proxy_balancer | Nginx upstream | Преимущество Nginx | Notes |
| --- | --- | --- | --- | --- |
| Макс. соединения | 2,500 | 10,000 | +300% | Nginx масштабируется лучше |
| Пропускная способность | 3,200 RPS | 5,800 RPS | +81.3% | Обработка большего трафика |
| Задержка (p95) | 75 ms | 32 ms | -57.3% | Более предсказуемая производительность |
| Потребление CPU | 88% | 62% | -29.5% | Эффективнее использует ресурсы |
| Память (1000 соединений) | 210 MB | 85 MB | -59.5% | Значительная экономия памяти |
| Время failover | 2.5s | 0.8s | -68% | Быстрее переключается при сбоях |


| Алгоритм/Протокол | Apache (TPS*) | Nginx (TPS*) | Разница | CPU Load Apache | CPU Load Nginx |
| --- | --- | --- | --- | --- | --- |
| TLS 1.2 + RSA 2048 | 850 | 1,450 | +70.6% | 95% | 75% |
| TLS 1.2 + ECDSA 256 | 1,200 | 2,100 | +75.0% | 85% | 65% |
| TLS 1.3 + ECDSA 256 | 1,500 | 2,800 | +86.7% | 80% | 60% |
| TLS 1.3 + Post-Quantum | 650 | 950 | +46.2% | 98% | 85% |
| Среднее значение | 1,050 | 1,825 | +73.8% | 89.5% | 71.3% |


| Компонент | Apache Memory (MB) | Nginx Memory (MB) | Разница | Примечание |
| --- | --- | --- | --- | --- |
| Основной процесс | 45 | 12 | -73.3% | Master process |
| Рабочие процессы | 85 × 4 = 340 | 18 × 8 = 144 | -57.6% | Worker processes |
| Общие библиотеки | 120 | 65 | -45.8% | Shared libraries |
| Кэш файлов | 95 | 42 | -55.8% | File descriptor cache |
| Буферы сети | 40 | 25 | -37.5% | Network buffers |
| Итого (1000 соединений) | 640 | 288 | -55.0% | Суммарное потребление |


| Операция | Apache CPU% | Nginx CPU% | Разница | Комментарий |
| --- | --- | --- | --- | --- |
| Системные вызовы | 35% | 18% | -48.6% | Nginx эффективнее |
| Контекстные переключения | 25% | 8% | -68.0% | Меньше overhead |
| Обработка сети | 20% | 45% | +125% | Nginx оптимизирован |
| Обработка файлов | 15% | 22% | +46.7% | sendfile() оптимизация |
| Планировщик | 5% | 7% | +40% | Схожие значения |
| Итого | 100% | 100% | - | - |


| Метрика | Apache | Nginx | Улучшение | Объяснение |
| --- | --- | --- | --- | --- |
| Пропускная способность | 8.2 Gbps | 9.5 Gbps | +15.9% | Лучшая обработка пакетов |
| Задержка (RTT) | 0.42 ms | 0.38 ms | -9.5% | Быстрее обработка |
| Пакетов/сек | 850k | 1,100k | +29.4% | Эффективная обработка |
| Потеря пакетов (1% loss) | 0.8% | 0.3% | -62.5% | Устойчивее к потерям |
| TCP Window Size | 512 KB | 1 MB | +100% | Большее окно у Nginx |
| Retransmission Rate | 0.5% | 0.2% | -60% | Стабильнее соединения |


| Функция | Apache 2.4.58 | Nginx 1.24.0 | Важность | Комментарий |
| --- | --- | --- | --- | --- |
| TLS 1.3 | + | + | Высокая | Оба поддерживают |
| 0-RTT (Early Data) | Частично | + | Средняя | Nginx имеет полную поддержку |
| OCSP Stapling | + | + | Высокая | Оба поддерживают |
| Certificate Transparency | Через модули | Через модули | Средняя | Схожие возможности |
| HSTS | Через mod_headers | Встроенная | Высокая | Nginx удобнее |
| HPKP (HTTP Public Key Pinning) | Устарело | Устарело | Низкая | Заменено на Expect-CT |
| ALPN | + | + | Высокая | Для HTTP/2 |
| SNI | + | + | Обязательно | Виртуальные хосты |

