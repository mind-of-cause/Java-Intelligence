create read update delete - основные операции в sql 
Пример работы с таблицей:
``` sql
insert into users (name, age, email) values('Alex', 22, 'alex@devcolibri.com');
select *from users;
select *from users where name = 'Steve';
select name, age from users where id = 2;
update users set name = 'Steve', age = 55 where id = 1;
delete from users where id = 4;

```
(create) insert - добавляет в таблицу **users** на место полей (name, age, email), значения values('Alex', 22, 'alex@devcolibri.com')
(read) select - показывает из **from** выбранной таблицы **users**; **where** выбор той строки, где есть поле **name** равное 'Steve' 
update - меняет значение в таблице **users** коммандой **set** поле **name** значением 'Steve', поле **age** значением 55, той строки **where** id = 1;
delete удаление