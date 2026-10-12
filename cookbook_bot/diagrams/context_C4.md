## 1. C4 Context — уровень 1

**Что показывает:** кто пользователь, что наша система, что снаружи.

```mermaid
graph TB
    User["👤 Пользователь<br/><i>ведёт список покупок<br/>дома или в команде</i>"]

    subgraph System["🍳 Cookbook System — граница системы"]
        direction TB
        Bot["🤖 cookbook_bot<br/><i>aiogram · Python<br/>Telegram-интерфейс<br/>тонкий клиент</i>"]
        API["🌐 cookbook_project<br/><i>Django REST API<br/>бизнес-логика и данные</i>"]
    end

    TG["📱 Telegram Bot API<br/><i>внешняя система<br/>доставка сообщений</i>"]
    DB[("🗄️ База данных<br/><i>PostgreSQL<br/>источник правды</i>")]

    User -->|"Telegram-клиент"| TG
    TG -->|"Bot API<br/>HTTPS"| Bot
    User -->|"Браузер<br/>HTTPS"| API
    Bot -->|"REST API<br/>HTTPS · X-Bot-Token"| API
    API -->|"SQL"| DB

    style System fill:#f8f9fa,stroke:#333,stroke-width:2px,stroke-dasharray: 5 5
    style Bot fill:#0088cc,color:#fff,stroke:#333
    style API fill:#0C4B33,color:#fff,stroke:#333
    style TG fill:#229ED9,color:#fff,stroke:#333
    style DB fill:#336791,color:#fff,stroke:#333
    style User fill:#fff,stroke:#333
```

**Ключевое:**
- **System Boundary** — пунктирная рамка вокруг бота и API.
- **Одна БД** — у Django. Бот **не хранит** состояние.
- **Стрелки:** `User → TG → Bot → API → DB`, `User → API` (браузер).
- **Протоколы подписаны:** `Bot API (HTTPS)`, `REST API (HTTPS, X-Bot-Token)`, `SQL`.


