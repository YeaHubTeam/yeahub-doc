# Сущность Chat

## Поля

1. **\_id**: тип - ObjectId, описание - Уникальный идентификатор чата
2. **Messages**: тип - Array, описание - массив связанных с чатом сообщений
3. **Members**: тип - Array, описание - массив связанных с чатом пользователей
4. **CreatedAt**: тип - Date, описание - дата создания чата

```json
{
  "_id": "ObjectId",
  "Messages": ["Messages"],
  "Members": ["Users"],
  "CreatedAt": "Date"
}
```

# Сущность Message

## Поля

1. **\_id**: тип - ObjectId, описание - Уникальный идентификатор сообщения
2. **ChatId**: тип - ObjectId, описание - Идентификатор чата связанный с сообщением
3. **Creator**: тип - ObjectId or String, описание - Автор сообщения
4. **Text**: тип - String, описание - Текст сообщения
5. **CreatedAt**: тип - Date, описание - Дата создания сообщения
6. **UpdatedAt**: тип - Date, описание - Дата обновления сообщения
7. **SeenAt**: тип - Date, описание - Дата просмотра сообщения 8. **Image**: тип - Buffer or String(ссылка на изображение), описание - изображение, добавленное пользователем

```json
{
  {
  "_id": "ObjectId",
  "ChatId": "ObjectId",
  "Creator": "ObjectId or String",
  "Text": "String",
  "CreatedAt": "Date",
  "UpdatedAt": "Date",
  "SeenAt": "Date",
  "Image": "Buffer or String (URL)"
}
}
```
