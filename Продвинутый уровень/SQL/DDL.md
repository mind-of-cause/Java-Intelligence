DDL (Data Definition Language) - это подкатегория SQL (Structured Query Language) и включает в себя команды, которые определяют структуру базы данных. Вот некоторые основные DDL-команды: 
1. `CREATE`: Эта команда используется для создания таблицы, индекса или представления в базе данных. Например, чтобы создать новую таблицу:
``` CREATE TABLE table_name ( column1 datatype constraint, column2 datatype constraint, ... ); ``` 
2. `DROP`: Команда `DROP` удаляет указанный объект, например таблицу или индекс, из базы данных. Например, чтобы удалить таблицу: ``` DROP TABLE table_name; ``` 
3. `ALTER`: Команда `ALTER` используется для модификации существующей таблицы. Это может быть добавление или удаление столбцов, изменение типа данных столбца и т.д. Например, чтобы добавить столбец в таблицу: ``` ALTER TABLE table_name ADD column_name datatype; ``` 
4. `TRUNCATE`: Команда `TRUNCATE` используется для удаления всех записей из таблицы, но при этом сохраняет саму структуру таблицы для будущего использования. Пример использования: ``` TRUNCATE TABLE table_name; ``` 
Помните, что DDL-команды влияют на структуру базы данных, и следует использовать их с осторожностью.