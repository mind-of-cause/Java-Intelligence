--
Область видимости:
- жизненный цикл бина
- возможное количество создаваемых бинов
Разновидности:
- singletone
- prototype
- request
- session
- global-session

Singletone 
-- 
Scope по умолчанию
- создаётся сразу после прочтения Spring Container-ом конфиг файла
- является общим для всех кто запросит у его Spring Container-а
- подходит для stateless объектов (без состояния)

Prototype
--
- такой бин создаётся только после обращения Spring Container'a к методу getBean();
- Для каждого обращения создаётся новый объект
- Подходит для stateful объектов (имеющих состояние)