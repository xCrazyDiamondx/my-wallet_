# MyWallet - прилоежние для отслеживания транзакций

Простое API
 позволяет добавлять транзакции "расход" и "доход". А так же выводит статистикку об истории транзаций и о текущем балансе.
 
## Установка
```bash
# установка зависимостей
pip install -r requirements.txt
# создание файла для хранения трназакций
echo "[]" > storage.json
```

## Запуск
```bash
python3 main.py --host 0.0.0.0 --port 8080

# Опции --host и --port позволяют сконфигурировать настройки Web-сервера
# Для просмотра всех опций выполните
python3 main.py --help
```

## API

Приложение запускает Web-сервер на Flask и обрабатывает 2 endpoint: получение статистики и добавление новой транзакции.
Тела запросов и ответов имеют формат JSON.
> Важно! Все POST запросы должны содержать заголовок `Content-type: application/json
>`, в противном случае сервер будет отвечать ошибкой.

### Добавление транзации
```bash
# Отправка POST запроса с JSON-телом
curl -X POST http://0.0.0.0:8080/add \
    -H 'Content-type: application/json'
    -d '{
        "type": "income",
        "value": 200.0,
        "description": "Зарплта"
    }'
```  
**Параметры запроса**
 - type - (обязательный, строка) тип транзации, должен принимать значения "income" или "outcome" 
 - value - (обязательный, число) сумма транзации 
 - description - (опциональный, строка) комментарий, описание транзакции

**Ответ**
В случае успеха запрос вернет HTTP 302 Found на страницу со статистикой
 
### Получение статистики
```bash
# Отправка GET запроса
curl -X GET http://0.0.0.0:8080/
```  
**Ответ**
 - balance - (обязательный, число) текущий баланс с учетом всех транзацкий 
 - transactions - (обязательный, cписок JSON-объектов):
     - timestamp - (обязательный, число) время создания транзации в формате UNIX timestamp 
     - type - (обязательный, строка) тип транзации, должен принимать значения "income" или "outcome" 
     - value - (обязательный, число) сумма транзации 
     - description - (опциональный, строка или null) комментарий, описание транзакции

# Автор
*Лебедев Фёдор(teoleb@inbox.ru)* 
 
  
