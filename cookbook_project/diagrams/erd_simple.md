```mermaid

erDiagram
    User ||--|| TelegramLink : "linked"
    User ||--o{ ShoppingList : "owns"
    User ||--o{ StorageItem : "owns"
    User ||--o{ PantryStaple : "tracks"
    User ||--o{ PurchaseLog : "logs"

    ShoppingList ||--o{ ShoppingListItem : "contains"
    ShoppingListItem }o--|| Ingredient : "references"
    ShoppingListItem }o--|| Unit : "measured in"

    StorageItem }o--|| Ingredient : "stored as"
    StorageItem }o--|| Unit : "measured in"

    PantryStaple }o--|| Ingredient : "staple of"

    Recipe ||--o{ RecipeIngredient : "has"
    RecipeIngredient }o--|| Ingredient : "uses"
    RecipeIngredient }o--|| Unit : "measured in"

    Recipe }o--o{ Diet : "compatible with"

    Ingredient }o--|| Unit : "default unit"

    User {
        int id PK
        string username UK
    }
    TelegramLink {
        int id PK
        int user FK
        bigint chat_id UK
    }
    ShoppingList {
        int id PK
        int user FK
        string title
    }
    ShoppingListItem {
        int id PK
        int shopping_list FK
        int ingredient FK
        decimal amount
        int unit FK
        bool is_bought
    }
    StorageItem {
        int id PK
        int user FK
        int ingredient FK
        decimal quantity
        int unit FK
        string location
        date expires_at
        string condition
    }
    PantryStaple {
        int id PK
        int user FK
        int ingredient FK
        string priority
        bool is_active
    }
    PurchaseLog {
        int id PK
        int user FK
        int ingredient FK
        decimal quantity
        int unit FK
        int storage_item FK
    }
    Recipe {
        int id PK
        string title
        string slug
        int servings
        int cooking_time
    }
    RecipeIngredient {
        int id PK
        int recipe FK
        int ingredient FK
        decimal amount
        int unit FK
    }
    Ingredient {
        int id PK
        string name
        string slug UK
        string type
        int default_unit FK
    }
    Unit {
        int id PK
        string name
        string abbreviation
        string kind
    }
    Diet {
        int id PK
        string slug UK
        string name
    }