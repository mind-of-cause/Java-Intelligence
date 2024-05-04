---
tags:
  - undone
---
execute() -- вставка, получение данных может давать несколько result set 'ов
executeUpdate() -- с помощью него выполняется insert, update, delete; можно делать запросы относительно таблиц, получать данные нельзя 
**Пример**:
```java
statement.executeUpdate("UPDATE animal SET anim_name='New Name' WHERE id=1;"); 
```
-
Возвращает кол-во записей в которые он внёс какие либо изменения int;

executeQuery() -- даёт возможность получить resultset можно выполнять только SELECT
**Пример:**
```java
Resultset res = statement.executeQuery("SELECT * FROM animal")
```

addBatch() -- возможность выполнить в пакете несколько запросов за одну команду execute
executeBatch() -- исполняет Batch'и
**Пример**:
```java
statement.addBatch ("INSERT INTO usertable(name, lastName, age) SET ('name1', 'lastName1', age1);");
statement.addBatch ("INSERT INTO usertable(name, lastName, age) SET ('name2', 'lastName2', age2);");
statement.addBatch ("INSERT INTO usertable(name, lastName, age) SET ('name3', 'lastName3', age3);");

statement.executeBatch();
```
clearBatch() -- стирает старые запросы из Batch и можно поместить новые;

getConnection() -- получение соединения к базе данных

Resultset resultSet -- объект, модель ответа запроса, полная модель таблицы, например