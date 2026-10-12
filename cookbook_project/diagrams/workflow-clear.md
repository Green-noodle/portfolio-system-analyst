# Workflow `/clear` — список покупок → склад

> Команда `/clear` в Telegram: пометить купленное, перенести в `StorageItem`,
> записать в `PurchaseLog`, очистить список.
> Реализация: `POST /api/bot/list/clear/` (v1.15).

```mermaid
sequenceDiagram
    autonumber
    participant U as 👤 Пользователь
    participant B as 🤖 Telegram-бот
    participant A as 🔌 Django API
    participant DB as 🐘 PostgreSQL
    
    U->>B: /clear
    B->>A: POST /api/bot/list/clear/<br/>{telegram_id}
    
    activate A
    A->>A: Проверить X-Bot-Token
    A->>DB: Найти TelegramLink по chat_id
    A->>DB: Найти активный ShoppingList
    
    Note over A: Если нет списка →<br/>{updated: 0, moved: 0, skipped: []}
    
    A->>DB: items.filter(is_bought=False)<br/>.update(is_bought=True)
    Note over A,DB: updated = N
    
    A->>A: move_bought_to_storage(user)
    
    loop Для каждой купленной позиции
        alt ingredient != null
            A->>DB: Создать StorageItem<br/>(ingredient, quantity, unit, location)
            A->>DB: Создать PurchaseLog<br/>(user, ingredient, quantity)
            Note over A: moved_to_storage++
        else ingredient == null
            Note over A: skipped.append(id)
        end
    end
    
    A->>DB: Удалить перенесённые ShoppingListItem
    A-->>B: {updated, moved_to_storage, skipped}
    deactivate A
    
    B-->>U: ✅ Перенесено 5 позиций<br/>Пропущено 2 (без ингредиента)
```