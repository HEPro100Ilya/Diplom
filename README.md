# Diplom

**Что ДЕЛАЕМ:**

- IDS/IPS на Suricata
    
- авто-бан по severity
    
- ручной бан через WebUI
    
- Telegram-уведомления
    
- VM без GUI
    
- WebUI по порту 8080
  
  **Что НЕ ДЕЛАЕМ:**

- ML
    
- LFS
    
- сложный фронт
    
- кластеризацию


Стек
1. Системный уровень (Core)
ОС: Debian 12
IDS/IPS: Suricata
Управление трафиком: iptables 
2. Бэкенд (Logic) 
Язык: Python 3.10+.
Web-фреймворк: FastAPI.
Работа с логами: Библиотека json и асинхронное чтение файлов 
БД: SQLite.
3. Фронтенд
Основа: HTML5, JavaScript (ES6+).
Стили: Tailwind CSS.
Графики: Chart.js.
4. Интеграции и связь
Уведомления: Telegram Bot API (библиотека aiogram).
Сервер приложений: Uvicorn (для запуска FastAPI).
Связь с ОС: Модуль subprocess (для выполнения команд iptables -A INPUT...).
Как это работает вместе:
Suricata мониторит сетевой интерфейс -> обнаруживает атаку -> пишет JSON-строку в eve.json.
Python-скрипт (Watcher) постоянно читает eve.json. Как только видит критический Priority, он:
Вызывает команду iptables для блокировки IP.
Пишет инцидент в SQLite.
Шлет сообщение в Telegram.
FastAPI отдает данные из SQLite на фронтенд.
Admin UI (браузер) отображает графики и позволяет админу вручную нажать кнопку "Разбанить" (что удаляет правило из iptables).
