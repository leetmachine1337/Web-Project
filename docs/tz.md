# Технічне завдання
Функційні вимоги:
1.	Перегляд каталогу товарів за групами – гість, клієнт – обов’язкова.
2.	Перегляд зображень товару на його сторінці – гість, клієнт – обов’язкова.
3.	Перегляд характеристик та опису товару – гість, клієнт - обов’язкова.
4.	Функціонал кошику – клієнт – обов’язкова.
5.	Створення замовлення без облікового запису (за номером телефону з перевіркою) – бажана.
6.	Реєстрація облікових записів та вхід – гість, клієнт – обов’язкова.
7.	Форма зворотного зв’язку – клієнт – бажана.
8.	Сповіщення про зміну ціни – клієнт – бажана.
9.	Функціонал знижок – адміністратор – обов’язкова.
10.	Перегляд списку облікових записів – адміністратор – обов’язкова.

Ролі користувачів:
1. Гість
2. Клієнт
3. Адміністратор

# ER-діаграма бази даних
```mermaid
erDiagram
    USERS {
        int id PK
        string role
        string first_name
        string last_name
        string email
        string password_hash
        string phone
        date birthday
        timestamp created_at
    }

    CATEGORIES {
        int id PK
        string name
        int parent_id FK
    }

    PRODUCTS {
        int id PK
        int category_id FK
        string name
        text description
        decimal price
        json attributes
    }

    PRODUCT_IMAGES {
        int id PK
        int product_id FK
        string image_url
        boolean is_main
    }

    CATEGORIES ||--o{ CATEGORIES : "parent_id (subcategories)"
    CATEGORIES ||--o{ PRODUCTS : "category_id"
    PRODUCTS ||--o{ PRODUCT_IMAGES : "product_id"