# Задание 1

<img width="1231" height="909" alt="test_ex1 drawio" src="https://github.com/user-attachments/assets/6f2f9e89-a348-4d91-af7d-c7fcad37e06a" />



# Задание 2



## Название

Публикация товара на витрине маркетплейса

## User Story

Как продавец, я хочу опубликовать свой товар на витрине маркетплейса, чтобы покупатели могли найти его в каталоге и оформить заказ.

## Критерии приемки 

* Продавец может выбрать товар из списка своих товаров.
* Система проверяет заполнение обязательных полей товара.
* Если обязательные поля не заполнены, система показывает список ошибок.
* Если все обязательные поля заполнены, товар переводится в статус **«На модерации»**.
* После успешного прохождения модерации товар публикуется на витрине.
* Продавец может видеть текущий статус публикации товара.
* При отклонении модерации продавец получает причину отказа.

# Use Case 1. Публикация товара на витрине


## Название

Публикация товара на витрине маркетплейса

## Актор

Продавец

## Предусловия

* Продавец авторизован в личном кабинете.
* Товар создан в системе.
* Товар находится в статусе **«Черновик»**.

## Основной сценарий

1. Продавец открывает список своих товаров.
2. Продавец выбирает товар.
3. Продавец нажимает кнопку **«Опубликовать на витрине»**.
4. Система выполняет проверку обязательных полей.
5. Система определяет, что все обязательные поля заполнены.
6. Система изменяет статус товара на **«На модерации»**.
7. Система отправляет товар на модерацию.
8. Система отображает уведомление об успешной отправке товара на модерацию.

## Постусловия

* Товар находится в статусе **«На модерации»**.

# Use Case 2. Ошибка публикации из-за незаполненных данных


## Название

Проверка обязательных полей товара

## Актор

Продавец

## Предусловия

* Продавец авторизован.
* Товар создан.

## Основной сценарий

1. Продавец нажимает кнопку **«Опубликовать на витрине»**.
2. Система проверяет обязательные поля.
3. Система обнаруживает незаполненные поля.
4. Система отображает сообщение об ошибке.
5. Система показывает перечень полей, требующих заполнения.
6. Продавец исправляет данные.

## Альтернативный поток

1. Продавец отказывается исправлять данные.
2. Товар остается в статусе **«Черновик»**.

## Постусловия

* Публикация не выполнена.

# Use Case 3. Завершение модерации


## Название

Обработка результата модерации

## Актор

Модератор (или система модерации)

## Предусловия

* Товар находится в статусе **«На модерации»**.

## Основной сценарий 

1. Модератор проверяет товар.
2. Модератор подтверждает публикацию.
3. Система меняет статус товара на **«Опубликован»**.
4. Товар становится доступным на витрине.
5. Продавец получает уведомление об успешной публикации.

## Альтернативный сценарий

1. Модератор отклоняет товар.
2. Указывает причину отклонения.
3. Система переводит товар в статус **«Требует доработки»**.
4. Продавец получает уведомление с причиной отказа.

## Постусловия

* Товар опубликован либо возвращен на доработку.

# Функциональные требования

| Номер   | Требование                                                                                         |
| ----- | -------------------------------------------------------------------------------------------------- |
| 1 | Система должна предоставлять возможность публикации товара через кнопку «Опубликовать на витрине». |
| 2 | Система должна проверять обязательные поля товара перед отправкой на модерацию.                    |
| 3 | Система должна отображать список ошибок при отсутствии обязательных данных.                        |
| 4 | Система должна присваивать товару статус «На модерации».                                           |
| 5 | Система должна сохранять историю изменения статусов товара.                                        |
| 6 | Система должна уведомлять продавца о результатах модерации.                                        |
| 7 | Система должна публиковать товар на витрине после успешной модерации.                              |
| 8 | Система должна сохранять причину отклонения товара при отказе в публикации.                        |



В PlantUML накидала диаграмму

<img width="494" height="449" alt="Снимок экрана 2026-06-25 в 21 26 53" src="https://github.com/user-attachments/assets/2b2c0f88-8986-4095-a641-07b55960ace1" />



# Задание 3

# Задание 3.1 REST API

## Описание


## HTTP-метод и URL

```http
POST /api/v1/users/register
Content-Type: application/json
```



## Входные параметры (тело запроса)

| Поле              | Тип    | Обязательность | Ограничения                                                                          |
| ----------------- | ------ | -------------- | ------------------------------------------------------------------------------------ |
| `first_name`      | string | Да             | 1–100 символов                                                                       |
| `last_name`       | string | Да             | 1–100 символов                                                                       |
| `username`        | string | Да             | 3–50 символов, только `[a-zA-Z0-9_]`                                                 |
| `password`        | string | Да             | 8–128 символов, содержит заглавную букву, строчную букву, цифру и специальный символ |
| `recaptcha_token` | string | Да             | Токен `g-recaptcha-response`, полученный от Google reCAPTCHA                         |



## Выходные параметры (успешный ответ, HTTP 201)

| Поле         | Тип               | Обязательность | Описание                              |
| ------------ | ----------------- | -------------- | ------------------------------------- |
| `user_id`    | UUID              | Да             | Уникальный идентификатор пользователя |
| `username`   | string            | Да             | Логин пользователя                    |
| `first_name` | string            | Да             | Имя                                   |
| `last_name`  | string            | Да             | Фамилия                               |
| `created_at` | string (ISO 8601) | Да             | Дата и время регистрации (UTC)        |
| `message`    | string            | Да             | `User registered successfully`        |



## Выходные параметры (ответ с ошибкой)

| Поле                | Тип           | Обязательность | Описание                                             |
| ------------------- | ------------- | -------------- | ---------------------------------------------------- |
| `error_code`        | string (enum) | Да             | Машиночитаемый код ошибки                            |
| `message`           | string        | Да             | Сообщение об ошибке                                  |
| `details`           | array         | Да             | Список ошибок по отдельным полям (может быть пустым) |
| `details[].field`   | string        | Нет            | Название поля                                        |
| `details[].message` | string        | Нет            | Описание ошибки                                      |



## Описание кодов ошибок

| HTTP    | `error_code`            | Тип        | Описание                                                                                          |
| ------- | ----------------------- | ---------- | ------------------------------------------------------------------------------------------------- |
| **400** | `VALIDATION_ERROR`      | Клиентская | Ошибка валидации входных данных. Для пароля используется текст ошибки, совпадающий с интерфейсом. |
| **400** | `RECAPTCHA_FAILED`      | Клиентская | `Please verify reCaptcha to register`                                                             |
| **409** | `USER_ALREADY_EXISTS`   | Клиентская | `User existed`                                                                                    |
| **500** | `INTERNAL_SERVER_ERROR` | Серверная  | `An unexpected error occurred. Please try again later.`                                           |



## Пример запроса

```http
POST /api/v1/users/register
Content-Type: application/json
```

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "username": "john_doe",
  "password": "Str0ng!Pass",
  "recaptcha_token": "03AGdBq26xyzABC..."
}
```


## Успешный ответ (201)

```json
{
  "user_id": "a3f5c812-7b2e-4d91-9c4a-001e2d3f4a5b",
  "username": "john_doe",
  "first_name": "John",
  "last_name": "Doe",
  "created_at": "2026-06-26T10:00:00Z",
  "message": "User registered successfully"
}
```



## Ответ при слабом пароле (400)

```json
{
  "error_code": "VALIDATION_ERROR",
  "message": "Validation failed",
  "details": [
    {
      "field": "password",
      "message": "Password must be at least 8 characters long and contain uppercase, lowercase, digit and special character"
    }
  ]
}
```



## Ответ при существующем пользователе (409)

```json
{
  "error_code": "USER_ALREADY_EXISTS",
  "message": "User existed",
  "details": []
}
```



## Ответ при непрохождении reCAPTCHA (400)

```json
{
  "error_code": "RECAPTCHA_FAILED",
  "message": "Please verify reCaptcha to register",
  "details": []
}
```

# Описание в формате openAPI

```
openapi: 3.0.0
info:
  title: User Registration API
  version: 1.0.0
  description: API для регистрации пользователей с валидацией и проверкой reCAPTCHA

paths:
  /api/v1/users/register:
    post:
      summary: Регистрация нового пользователя
      description: Создаёт новую учётную запись пользователя с валидацией, проверкой сложности пароля и верификацией reCAPTCHA
      operationId: registerUser
      tags:
        - Users
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/RegistrationRequest'
            examples:
              validRequest:
                summary: Пример корректного запроса на регистрацию
                value:
                  first_name: "John"
                  last_name: "Doe"
                  username: "john_doe"
                  password: "Str0ng!Pass"
                  recaptcha_token: "03AGdBq26xyzABC..."
      responses:
        '201':
          description: Пользователь успешно зарегистрирован
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/RegistrationResponse'
              example:
                user_id: "a3f5c812-7b2e-4d91-9c4a-001e2d3f4a5b"
                username: "john_doe"
                first_name: "John"
                last_name: "Doe"
                created_at: "2026-06-26T10:00:00Z"
                message: "User registered successfully"
        '400':
          description: Неверный запрос - ошибка валидации или ошибка reCAPTCHA
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
              examples:
                validationError:
                  summary: Ошибка валидации пароля
                  value:
                    error_code: "VALIDATION_ERROR"
                    message: "Validation failed"
                    details:
                      - field: "password"
                        message: "Password must be at least 8 characters long and contain uppercase, lowercase, digit and special character"
                recaptchaError:
                  summary: Ошибка верификации reCAPTCHA
                  value:
                    error_code: "RECAPTCHA_FAILED"
                    message: "Please verify reCaptcha to register"
                    details: []
        '409':
          description: Конфликт - пользователь уже существует
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
              example:
                error_code: "USER_ALREADY_EXISTS"
                message: "User existed"
                details: []
        '500':
          description: Внутренняя ошибка сервера
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
              example:
                error_code: "INTERNAL_SERVER_ERROR"
                message: "An unexpected error occurred. Please try again later."
                details: []

components:
  schemas:
    RegistrationRequest:
      type: object
      required:
        - first_name
        - last_name
        - username
        - password
        - recaptcha_token
      properties:
        first_name:
          type: string
          description: Имя пользователя
          minLength: 1
          maxLength: 100
          example: "John"
        last_name:
          type: string
          description: Фамилия пользователя
          minLength: 1
          maxLength: 100
          example: "Doe"
        username:
          type: string
          description: Уникальное имя пользователя (логин)
          pattern: '^[a-zA-Z0-9_]+$'
          minLength: 3
          maxLength: 50
          example: "john_doe"
        password:
          type: string
          description: |
            Пароль должен содержать от 8 до 128 символов и включать:
            - Как минимум одну заглавную букву
            - Как минимум одну строчную букву
            - Как минимум одну цифру
            - Как минимум один специальный символ
          minLength: 8
          maxLength: 128
          pattern: '^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#$%^&*(),.?":{}|<>]).+$'
          example: "Str0ng!Pass"
        recaptcha_token:
          type: string
          description: Токен Google reCAPTCHA (g-recaptcha-response)
          example: "03AGdBq26xyzABC..."

    RegistrationResponse:
      type: object
      required:
        - user_id
        - username
        - first_name
        - last_name
        - created_at
        - message
      properties:
        user_id:
          type: string
          format: uuid
          description: Уникальный идентификатор пользователя
          example: "a3f5c812-7b2e-4d91-9c4a-001e2d3f4a5b"
        username:
          type: string
          description: Логин пользователя
          example: "john_doe"
        first_name:
          type: string
          description: Имя пользователя
          example: "John"
        last_name:
          type: string
          description: Фамилия пользователя
          example: "Doe"
        created_at:
          type: string
          format: date-time
          description: Дата и время регистрации (UTC)
          example: "2026-06-26T10:00:00Z"
        message:
          type: string
          description: Сообщение об успешной регистрации
          example: "User registered successfully"

    ErrorResponse:
      type: object
      required:
        - error_code
        - message
        - details
      properties:
        error_code:
          type: string
          description: Машиночитаемый код ошибки
          enum:
            - VALIDATION_ERROR
            - RECAPTCHA_FAILED
            - USER_ALREADY_EXISTS
            - INTERNAL_SERVER_ERROR
          example: "VALIDATION_ERROR"
        message:
          type: string
          description: Сообщение об ошибке
          example: "Validation failed"
        details:
          type: array
          description: Список ошибок по отдельным полям (может быть пустым)
          items:
            $ref: '#/components/schemas/ErrorDetail'
          example: []

    ErrorDetail:
      type: object
      properties:
        field:
          type: string
          description: Название поля
          example: "password"
        message:
          type: string
          description: Описание ошибки
          example: "Password must be at least 8 characters long and contain uppercase, lowercase, digit and special character"

  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

security: []

```

# Задание 3.2 — Алгоритм создания пользователя на бэкенде


### Шаг 1. Разбор тела запроса

Получить HTTP-запрос и десериализовать входящий JSON. Если тело запроса не является корректным JSON, вернуть:

* HTTP **400 Bad Request**.


### Шаг 2. Проверка обязательных полей

Проверить наличие следующих полей:

* `first_name`
* `last_name`
* `username`
* `password`
* `recaptcha_token`

Если хотя бы одно поле отсутствует или пустое — вернуть:

* HTTP **400**
* `VALIDATION_ERROR`

с указанием ошибок в массиве `details`.


### Шаг 3. Валидация форматов

Проверить:

* `username` — длина 3–50 символов;
* допустимые символы — только `[a-zA-Z0-9_]`;
* `first_name` и `last_name` — длина от 1 до 100 символов.

При нарушении вернуть:

* HTTP **400**
* `VALIDATION_ERROR`.



### Шаг 4. Проверка сложности пароля

Проверить пароль по правилам:

* минимум 8 символов;
* минимум одна заглавная буква;
* минимум одна строчная буква;
* минимум одна цифра;
* минимум один специальный символ.

При несоответствии вернуть:

* HTTP **400**
* `VALIDATION_ERROR`

с сообщением, совпадающим с текстом ошибки в пользовательском интерфейсе.



### Шаг 5. Проверка Google reCAPTCHA

Отправить POST-запрос на сервис Google:

```
https://www.google.com/recaptcha/api/siteverify
```

Передать:

* секретный ключ сервера;
* `recaptcha_token`.

Если Google возвращает:

```json
{
  "success": false
}
```

вернуть:

* HTTP **400**
* `RECAPTCHA_FAILED`.



### Шаг 6. Проверка уникальности пользователя

Выполнить запрос к базе данных:

```sql
SELECT * FROM users
WHERE username = :username;
```

Если пользователь найден:

* HTTP **409 Conflict**
* `USER_ALREADY_EXISTS`
* сообщение `User existed`.


### Шаг 7. Хеширование пароля

Перед сохранением сформировать криптографический хеш пароля с использованием алгоритма:

* **bcrypt**

В базе данных хранится только хеш пароля. Исходный пароль никогда не сохраняется.


### Шаг 8. Сохранение пользователя

В рамках транзакции выполнить вставку записи:

```sql
INSERT INTO users
(
    first_name,
    last_name,
    username,
    password_hash,
    created_at
)
VALUES (...);
```

Во время сохранения:

* генерируется `UUID`;
* фиксируется время создания пользователя (`created_at`).


### Шаг 9. Обработка ошибок базы данных

Если при выполнении транзакции возникла ошибка (например:

* недоступность БД;
* таймаут;
* нарушение уникального индекса;
* race condition),

необходимо выполнить откат транзакции и вернуть:

```text
HTTP 500 Internal Server Error
```

с кодом

```text
INTERNAL_SERVER_ERROR
```


### Шаг 10. Формирование успешного ответа

При успешном завершении регистрации вернуть:

* HTTP **201 Created**

с телом ответа:

* `user_id`
* `username`
* `first_name`
* `last_name`
* `created_at`
* `message = "User registered successfully"`

# Описание в виде диаграммы:
<img width="2624" height="6097" alt="user_registration_backend_algorithm" src="https://github.com/user-attachments/assets/ec44b156-dd84-4fc6-9961-522e3644fc6f" />


