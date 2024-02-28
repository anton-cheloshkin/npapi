# Подать объявление
```
POST https://35media.ru/npapi/v1/offer
```
```json
{
  "text": "Текст объявления",
  "personName": "ANTON CHELOSHKIN",
  "email": "cheloshkin.anton@gmail.com",
  "phone": "8 (906) 299-99-88",
  //даты списком, это даты выхода газет
  "issues": ["2024-03-06T00:00"], // Локальяна дата По МОСКВЕ!!!, без Z
  "target": "rech", // "rech"|"golos"
  "countWords": 1,
  "isBordered": true,
  "pricePerWord": 16,
  "total": 100
}
```
Получаем в ответ номер объявление, 
```json
{
  "id": "3291ee50-0e87-4ccb-a9b3-07dec136e76a"
}
```
# Создать платеж
```
POST https://35media.ru/npapi/v1/payment/pay
```
```json
{
  "key": "3291ee50-0e87-4ccb-a9b3-07dec136e76a"
}
```
Получаем в ответ
```json
{
  "url": "https://yoomoney.ru/checkout/payments/v2/contract?orderId=2d7152f3-000f-5000-8000-179f87a71689"
}
```
И отправляем пользователя оплачивать
# После успешной оплаты нас Юкасса отправит на страницу
```
https://35media.ru/store/finish?id=3291ee50-0e87-4ccb-a9b3-07dec136e76a
```
# Чекаем
```
GET https://35media.ru/npapi/v1/payment/finish/3291ee50-0e87-4ccb-a9b3-07dec136e76a
```

И получаем в ответ plain text


- success -- платеж успешно проверен и записан
- paid -- платеж уже был зарегистрирован

Ошибка 400 - все другие исходы

