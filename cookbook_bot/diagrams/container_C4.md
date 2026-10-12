## 2. C4 Container — уровень 2

**Что показывает:** из чего состоит система внутри — контейнеры, слои, два репозитория.

```mermaid
graph TB
    User["👤 Пользователь"]

    subgraph System["🍳 Cookbook System"]
        direction TB

        subgraph BotRepo["📦 cookbook_bot — репозиторий 1"]
            Handlers["🎛️ Handlers<br/><i>aiogram · Python<br/>/add /list /remove /clear<br/>/export /bought</i>"]
            Client["🔌 API Client<br/><i>httpx + tenacity<br/>retry, обработка ошибок</i>"]
            Schemas["📋 Schemas<br/><i>Pydantic<br/>валидация контракта</i>"]
            Parsing["🧩 Parsing<br/><i>utils/parsing.py<br/>чистые функции</i>"]
        end

        subgraph ApiRepo["📦 cookbook_project — репозиторий 2"]
            DRF["🌐 Django REST API<br/><i>drf-spectacular<br/>/api/bot/*</i>"]
            Models["🗃️ Django Models<br/><i>Ingredient · ShoppingItem · Unit</i>"]
            Admin["🖥️ Django Admin<br/><i>управление данными</i>"]
        end
    end

    TG["📱 Telegram Bot API"]
    DB[("🗄️ PostgreSQL<br/><i>источник правды</i>")]
    CI["⚙️ GitHub Actions<br/><i>ruff · pytest · Codecov</i>"]

    User -->|"Telegram-клиент"| TG
    TG -->|"Bot API (HTTPS)"| Handlers
    User -->|"HTTPS, браузер"| DRF
    User -->|"HTTPS"| Admin

    Handlers --> Client
    Client --> Schemas
    Handlers --> Parsing

    Client -->|"REST API<br/>HTTPS · X-Bot-Token"| DRF
    DRF --> Models
    Models -->|"SQL"| DB
    Admin --> Models

    BotRepo -.->|"CI"| CI
    ApiRepo -.->|"CI"| CI

    style System fill:#f8f9fa,stroke:#333,stroke-width:2px,stroke-dasharray: 5 5
    style BotRepo fill:#e7f3ff,stroke:#0088cc,stroke-width:2px
    style ApiRepo fill:#e8f5ee,stroke:#0C4B33,stroke-width:2px
    style Handlers fill:#0088cc,color:#fff
    style Client fill:#4da6d9,color:#fff
    style Schemas fill:#7fc1e6,color:#000
    style Parsing fill:#a8d5f0,color:#000
    style DRF fill:#0C4B33,color:#fff
    style Models fill:#1a6b4a,color:#fff
    style Admin fill:#2d8a63,color:#fff
    style TG fill:#229ED9,color:#fff
    style DB fill:#336791,color:#fff
    style CI fill:#24292e,color:#fff
```

**Ключевое:**
- **Две рамки** — два репозитория (разный цвет).
- **Внутри бота** — 4 слоя: `Handlers → Client → Schemas`, `Handlers → Parsing`.
- **Внутри API** — `DRF → Models → DB`, `Admin → Models`.
- **CI** — общий для двух репо.
- **Одна БД** — только у Django.

