# Orders API

Сервис заказов. OAS 3.1, версия 0.1.0.

## POST /orders

Создать заказ.

Request body:

```json
{
  "account_id": 0,
  "item": "string",
  "quantity": 1
}
```

Responses:

- `201` — карточка заказа:

  ```json
  {
    "id": 0,
    "account_id": 0,
    "item": "string",
    "quantity": 1,
    "status": "string"
  }
  ```

- `422` — Validation Error (стандартный формат FastAPI):

  ```json
  {
    "detail": [
      {
        "loc": ["body", "account_id"],
        "msg": "string",
        "type": "string",
        "input": "string",
        "ctx": {}
      }
    ]
  }
  ```

- `404` — аккаунт не найден (после задачи 1.5)
- `503` — сервис клиентов недоступен (после задачи 1.5)

## GET /orders/{order_id}

Получить заказ по идентификатору.

Path parameters:

- `order_id` (integer, обязательный)

Responses:

- `200` — карточка заказа (та же схема, что и в ответе `POST /orders`)
- `404` — заказ не найден
- `422` — Validation Error

## GET /orders

Список заказов.

Query parameters:

- `account_id` (integer, опциональный) — фильтр по клиенту
- `limit` (integer, default 50, min 1, max 200)

Responses:

- `200` — массив карточек заказов (`[]`, если пусто)
- `422` — Validation Error

## GET /health

Жив ли сервис. Намеренно не обращается к базе данных — должен отвечать быстро и всегда.

Responses:

- `200`:

  ```json
  {
    "status": "string",
    "service": "string"
  }
  ```
