## 4. Sequence — `/list` + toggle

**Что показывает:** callback-flow и правило «`callback.answer()` первым».

```mermaid
sequenceDiagram
    autonumber
    actor U as 👤 User
    participant TG as 📱 Telegram
    participant H as 🎛️ Handler /list
    participant C as 🔌 API Client
    participant API as 🌐 Django API

    U->>TG: /list
    TG->>H: message
    H->>C: get_list(telegram_id)
    C->>API: GET /api/bot/list/?telegram_id=...
    API-->>C: {items: [...]}
    C-->>H: ShoppingListDTO
    H-->>TG: список + inline-кнопки toggle
    TG-->>U: 📋 Список (1 из 3)<br/>[✓] toggle:42

    U->>TG: нажатие toggle:42
    TG->>H: callback_query
    H->>H: await callback.answer()
    H->>C: toggle_item(42, telegram_id)
    C->>API: POST /api/bot/items/42/toggle/
    API-->>C: {id: 42, is_bought: true}
    H->>C: get_list(telegram_id)
    C->>API: GET /api/bot/list/?telegram_id=...
    API-->>C: {items: [...]}
    H-->>TG: edit_text + edit_reply_markup
    TG-->>U: обновлённый список
```

---

## 🗂 Легенда

| Иконка | Что |
|---|---|
| 👤 | Пользователь |
| 🤖 | `cookbook_bot` — Telegram-бот (aiogram) |
| 🌐 | `cookbook_project` — Django REST API |
| 🗄️ | PostgreSQL — источник правды |
| 📱 | Telegram Bot API — внешняя система |
| ⚙️ | GitHub Actions — CI |
| 🎛️ | Handlers — слой aiogram |
| 🔌 | API Client — httpx + tenacity |
| 📋 | Schemas — Pydantic |
| 🧩 | Parsing — чистые функции |
| 🗃️ | Django Models |
| 🖥️ | Django Admin |