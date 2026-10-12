```mermaid

erDiagram
    LogEntry {
        int id PK
        int user FK
        int content_type FK
    }
    Group {
        int id PK
        varchar name UK
    }
    Permission {
        int id PK
        int content_type FK
    }
    User {
        int id PK
        varchar username UK
    }
    Token {
        varchar key PK
        int user FK
    }
    ContentType {
        int id PK
    }
    Category {
        bigint id PK
        slug slug UK
    }
    ComboRating {
        bigint id PK
        bigint combo FK
        int user FK
    }
    ComboRecipe {
        bigint id PK
        bigint combo_set FK
        bigint recipe FK
    }
    ComboScenario {
        bigint id PK
        slug slug UK
    }
    ComboScenarioItem {
        bigint id PK
        bigint scenario FK
        bigint combo_set FK
    }
    ComboSet {
        bigint id PK
        bigint main_ingredient FK
        bigint meal_type FK
    }
    CookingMethod {
        bigint id PK
        varchar name UK
    }
    Diet {
        bigint id PK
        slug slug UK
    }
    DietRecommendation {
        bigint id PK
        bigint diet FK
    }
    Favorite {
        bigint id PK
        int user FK
        bigint recipe FK
    }
    GlycemicIndex {
        bigint id PK
        bigint ingredient FK
    }
    Ingredient {
        bigint id PK
        varchar name UK
        slug slug UK
        bigint default_unit FK
        bigint bought_unit FK
        bigint storage_unit FK
        bigint recipe_unit FK
    }
    IngredientNutritionByMethod {
        bigint id PK
        bigint ingredient FK
        bigint cooking_method FK
        bigint nutritional_value FK
    }
    IngredientSubstitute {
        bigint id PK
        bigint original FK
        bigint substitute FK
    }
    IngredientTip {
        bigint id PK
        bigint ingredient FK
        int author FK
        int moderated_by FK
    }
    MealTime {
        bigint id PK
        varchar name UK
    }
    MealType {
        bigint id PK
        varchar name UK
    }
    NutritionalValue {
        bigint id PK
        bigint ingredient FK
    }
    PantryStaple {
        bigint id PK
        int user FK
        bigint ingredient FK
    }
    PurchaseLog {
        bigint id PK
        int user FK
        bigint ingredient FK
        bigint unit FK
        bigint storage_item FK
    }
    Recipe {
        bigint id PK
        int author FK
        bigint category FK
        bigint meal_type FK
        bigint meal_time FK
    }
    RecipeIngredient {
        bigint id PK
        bigint recipe FK
        bigint ingredient FK
        bigint unit FK
        bigint cooking_method FK
    }
    RecipeTip {
        bigint id PK
        bigint recipe FK
        int author FK
        int moderated_by FK
    }
    ShoppingList {
        bigint id PK
        int user FK
    }
    ShoppingListItem {
        bigint id PK
        bigint shopping_list FK
        bigint ingredient FK
        bigint unit FK
    }
    StorageItem {
        bigint id PK
        int user FK
        bigint ingredient FK
        bigint unit FK
    }
    Supply {
        bigint id PK
        varchar name UK
        slug slug UK
    }
    Tag {
        bigint id PK
        varchar name UK
    }
    TelegramLink {
        bigint id PK
        int user FK
        bigint chat_id UK
    }
    TipVote {
        bigint id PK
        int user FK
        bigint recipe_tip FK
        bigint ingredient_tip FK
    }
    Unit {
        bigint id PK
    }
    Session {
        varchar session_key PK
    }
    Profile {
        bigint id PK
        int user FK
    }

    ComboSet ||--o{ ComboRating : "fk"
    User ||--o{ ComboRating : "fk"
    ComboSet ||--o{ ComboRecipe : "fk"
    Recipe ||--o{ ComboRecipe : "fk"
    ComboScenario ||--o{ ComboScenarioItem : "fk"
    ComboSet ||--o{ ComboScenarioItem : "fk"
    Ingredient ||--o{ ComboSet : "fk"
    MealType ||--o{ ComboSet : "fk"
    Diet ||--o{ DietRecommendation : "fk"
    Recipe ||--o{ Favorite : "fk"
    User ||--o{ Favorite : "fk"
    Ingredient ||--|| GlycemicIndex : "o2o"
    Unit ||--o{ Ingredient : "fk"
    CookingMethod ||--o{ IngredientNutritionByMethod : "fk"
    Ingredient ||--o{ IngredientNutritionByMethod : "fk"
    NutritionalValue ||--o{ IngredientNutritionByMethod : "fk"
    Ingredient ||--o{ IngredientSubstitute : "fk"
    Ingredient ||--o{ IngredientTip : "fk"
    User ||--o{ IngredientTip : "fk"
    ContentType ||--o{ LogEntry : "fk"
    User ||--o{ LogEntry : "fk"
    Ingredient ||--o{ NutritionalValue : "fk"
    Ingredient ||--o{ PantryStaple : "fk"
    User ||--o{ PantryStaple : "fk"
    ContentType ||--o{ Permission : "fk"
    User ||--|| Profile : "o2o"
    Ingredient ||--o{ PurchaseLog : "fk"
    StorageItem ||--o{ PurchaseLog : "fk"
    Unit ||--o{ PurchaseLog : "fk"
    User ||--o{ PurchaseLog : "fk"
    Category ||--o{ Recipe : "fk"
    MealTime ||--o{ Recipe : "fk"
    MealType ||--o{ Recipe : "fk"
    User ||--o{ Recipe : "fk"
    CookingMethod ||--o{ RecipeIngredient : "fk"
    Ingredient ||--o{ RecipeIngredient : "fk"
    Recipe ||--o{ RecipeIngredient : "fk"
    Unit ||--o{ RecipeIngredient : "fk"
    Recipe ||--o{ RecipeTip : "fk"
    User ||--o{ RecipeTip : "fk"
    User ||--o{ ShoppingList : "fk"
    Ingredient ||--o{ ShoppingListItem : "fk"
    ShoppingList ||--o{ ShoppingListItem : "fk"
    Unit ||--o{ ShoppingListItem : "fk"
    Ingredient ||--o{ StorageItem : "fk"
    Unit ||--o{ StorageItem : "fk"
    User ||--o{ StorageItem : "fk"
    User ||--|| TelegramLink : "o2o"
    IngredientTip ||--o{ TipVote : "fk"
    RecipeTip ||--o{ TipVote : "fk"
    User ||--o{ TipVote : "fk"
    User ||--|| Token : "o2o"
