**  

[Конспекты для подготовки к ревью core, pp](https://drive.google.com/drive/folders/1rPKSGI7m1NoFO4BxszBW6adMb28PaXuS?usp=sharing).

Конспекты правим в режиме онлайн, для этого открыли вам комментарии.

  

dis: [Kata inside](https://discord.com/invite/fEGCkHTe)

# SPRING BOOT, SPRING SECURITY и REST

- ### Spring security
    

Это фреймворк, набор фильтров сервлетов, которые помогают добавить аутентификацию, авторизацию и защиту от распространенных атак в веб-приложение.

Модуль Spring Security позволяет внедрять права доступа, а также контролировать их исполнение без ручных проверок.

Базируется на двух интерфейсах, которые определяют связь сущностей с секьюрностью: UserDetails и GrantedAuthority.

  
UserDetails - то, что будет интерпретироваться системой как пользователь.

GrantedAuthority - сущность, описывающая права юзера.

  

Аутентификация и авторизация должны быть на уровне фильтров до выполнения любой иной логики приложения.

  

- ### Связи таблиц
    

- Один к одному (@OneToOne)

Данный тип связей встречается не часто. В этом случае объекту одной сущности можно сопоставить только один объект другой сущности. Например, на некоторых сайтах пользователь может иметь только один блог. То есть возникает отношение один пользователь - один блог.

Нередко этот тип связей предполагает разбиение одной большой таблицы на несколько маленьких. Основная родительская таблица в этом случае продолжает содержать часто используемые данные, а дочерняя зависимая таблица обычно хранит данные, которые используются реже.

В этом отношении первичный ключ зависимой таблицы в то же время является внешним ключом, который ссылается на первичный ключ из главной таблицы.

- Многие ко многим (@ManyToMany)

При этом типе связей одна строка из таблицы А может быть связана с множеством строк из таблицы В. В свою очередь одна строка из таблицы В может быть связана с множеством строк из таблицы А. Типичный пример - студенты и курсы: один студент может посещать несколько курсов, и соответственно на один курс могут записаться несколько студентов.

Другой пример - статьи и теги: для одной статьи можно определить несколько тегов, а один тег может быть определен для нескольких статей.

Но в SQL Server на уровне базы данных мы не можем установить прямую связь многие ко многим между двумя таблицами. Это делается посредством вспомогательной промежуточной таблицы. Иногда данные из этой промежуточной таблицы представляют отдельную сущность.

  

- Один ко многим (@OneToMany):

Этот тип связи означает, что каждая строка в одной таблице может быть связана с несколькими строками в другой таблице, но каждая строка во второй таблице связана только с одной строкой в первой таблице.

Пример: Один автор может иметь несколько книг, но каждая книга принадлежит только одному автору.

Обычно реализуется путем добавления внешнего ключа в таблицу, которая является "многим" в отношении.

  

Один ко многим (Bidirectional) (@ManyToOne):

  

Этот тип связи является обратной стороной от "Один ко многим (@OneToMany)" и подразумевает, что каждая строка во второй таблице связана с одной строкой в первой таблице.

Пример: Каждая книга принадлежит только одному автору, но автор может иметь несколько книг.

В этом случае, помимо внешнего ключа в таблице "многих", также устанавливается связь с таблицей "одного".

  

Один к нулю или один (Optional) (@OneToOne with optional = true):

  

Этот тип связи похож на "Один к одному", но предполагает, что связанный объект может отсутствовать (null).

Пример: Паспорт и человек. Не у всех людей может быть паспорт, и паспорт может быть привязан только к одному человеку.

  
  
## Q
- ### Каскады для таблиц и какие они бывают?
    
## A
Каскадные типы используются для того, чтобы показать, как должны себя вести связанные данные при использовании специфических методов на целевую сущность.

Стандарт JPA подразумевает использование шести видов каскадности:

- PERSIST (Создание):

Операции сохранения (create) будут каскадно применяться ко всем связанным сущностям. Если вы сохраняете основную сущность, связанные сущности также будут сохранены в базе данных, если их там еще нет.

- MERGE (Обновление):

Операции обновления (update) будут каскадно применяться ко всем связанным сущностям. Если вы обновляете основную сущность, связанные сущности также будут обновлены.

- REMOVE (Удаление):

Операции удаления (delete) будут каскадно применяться ко всем связанным сущностям. Если вы удаляете основную сущность, связанные сущности также будут удалены.
  
- REFRESH (Обновление из базы данных):

Каскадное обновление из базы данных. Это означает, что если основная сущность обновляется из базы данных, связанные сущности также будут обновлены.

Основное различие с MERGE заключается в том, что MERGE применяется для слияния изменений из отсоединенной сущности в базу данных, тогда как REFRESH используется для обновления состояния управляемой сущности из базы данных.

  

DETACH (Отсоединение):

Отсоединение от контекста хранения. Если вы отсоединяете основную сущность, связанные сущности также будут отсоединены.

  

ALL (Все вышеперечисленные):

Каскадно применяет все операции: PERSIST, MERGE, REMOVE, REFRESH, DETACH.

  

Пример использования аннотации CascadeType:

  

@OneToOne(cascade = CascadeType.ALL)

@JoinColumn(name = "address_id", referencedColumnName = "id")

private Address address;

  

В данном примере для отношения "один к одному" указан каскадный тип ALL, что означает применение всех операций каскада для связанной сущности Address.

# Spring security

Это фреймворк, набор фильтров сервлетов, которые помогают добавить аутентификацию, авторизацию и защиту от распространенных атак в веб-приложение.

  

Модуль Spring Security позволяет внедрять права доступа, а также контролировать их исполнение без ручных проверок.

Базируется на двух интерфейсах, которые определяют связь сущностей с секьюрностью: UserDetails и GrantedAuthority.

UserDetails - то, что будет интерпретироваться системой как пользователь.

GrantedAuthority - сущность, описывающая права юзера.

Аутентификация и авторизация должны на уровне фильтров до выполнения любой иной логики приложения.

  

## Авторизация, аутентификация.

Аутентификация — процедура проверки подлинности, например проверка подлинности пользователя путем сравнения введённого им пароля с паролем, сохраненным в базе данных. 

  

Авторизация — предоставление определённому лицу или группе лиц прав на выполнение определенных действий.

  

## Процесс получения доступа.

Прежде чем попасть в контроллер, запрос проходит через цепочку фильтров. UsernamePasswordAuthenticationFilter получает имя и пароль и формирует объект Authentication. Имя хранится в поле principal, а пароль - credenticals (строковое представление), isAuthenticated() устанавливается в false

На следующем этапе AuthenticationManager при помощи единственного метода authenticate() выполняет аутентификацию, сама проверка делегируется конкретным провайдерам (In-Memory,  Jdbc, LDAP и др - в зависимости от того, как хранится реальный пользователь).

Если аутентификация не прошла (имя и пароль неверны), то выбрасывается исключение BadCredentials.

В случае же успеха возвращается тоже объект Authentication,  но заполненный по-другому: в поле Principal объекта Authentication будет реальный пользователь в виде UserDetails (сюда перемещаются имя и пароль), поле Credentials обнуляется, а isAuthenticated() меняется с false на true.

  

## In Memory Authentication от basic Authentication?

Basic Authentication представляет собой процедуру обмена конфиденциальной информацией (имя пользователя и пароль) для получения доступа к защищенным частям сайта или приложения.

  

In-Memory Authentication - механизм использования временной базы данных, которая остается в оперативной памяти приложения.

  

## Секьюрность контроллеров (минимум 2 способа)

Аннотации:

1. @Secured (одна и более ролей) и @RolesAllowed (одна роль)
    

|   |
|---|
|@Secured({ "ROLE_VIEWER", "ROLE_EDITOR" })  <br>public boolean isValidUsername(String username) {  <br>    return userRoleRepository.isValidUsername(username);  <br>}|

  

|   |
|---|
|@RolesAllowed("ROLE_VIEWER")  <br>public String getUsername2() {  <br>    //...  <br>}|

2. @PreAuthorize и @PostAuthorize (обеспечивают управление доступом на основе выражений SpEL (Spring Expression Language) до  и после выполнения аннотированного метода )
    

|   |
|---|
|@PreAuthorize("hasRole('ROLE_VIEWER')")  <br>public String getUsernameInUpperCase() {  <br>    return getUsername().toUpperCase();  <br>}|

  

|   |
|---|
|@PostAuthorize("#username == authentication.principal.username")  <br>public String getMyRoles2(String username) {  <br>    //...  <br>}|

3. @PreFilter и @PostFilter (обеспечивают фильтрацию коллекции, переданной в качестве аргумента до и после выполнения аннотированного метода)
    

|   |
|---|
|@PreFilter("filterObject != authentication.principal.username")  <br>public String joinUsernames(List<String> usernames) {  <br>    return usernames.stream().collect(Collectors.joining(";"));  <br>}|

  

|   |
|---|
|@PostFilter("filterObject != authentication.principal.username")  <br>public List<String> getAllUsernamesExceptCurrent() {  <br>    return userRoleRepository.getAllUsernames();  <br>}|

  

# Bootstrap.

Cвободный набор инструментов (CSS-фреймворк) для создания сайтов и веб-приложений. Включает в себя HTML и CSS-шаблоны оформления для типографики, веб-форм, кнопок, меток, блоков навигации и прочих компонентов веб-интерфейса, включая JavaScript-расширения.

  

Основные инструменты Bootstrap:

Сетки — заранее заданные размеры колонок, которые можно сразу же использовать, например, ширина колонки 140 px относится к классу .span2 (.col-md-2 в третьей версии фреймворка), который можно использовать в CSS-описании документа.

Шаблоны — фиксированный или резиновый шаблон документа.

Типографика — описания шрифтов, определение некоторых классов для шрифтов, таких как

код, цитаты и т. п.

Медиа — предоставляет некоторое управление изображениями и видео.

Таблицы — средства оформления таблиц, вплоть до добавления функциональности сортировки.

Формы — классы для оформления форм и некоторых событий, происходящих с ними.

Навигация — классы оформления для панелей, вкладок, перехода по страницам, меню и панели инструментов.

Алерты — оформление диалоговых окон, подсказок и всплывающих окон.

  

# Rest-сервисы.

REST — архитектурный стиль построения веб-сервисов, чаще всего используемый для API. По сути, это набор соглашений, позволяющих стандартизировать работу с системой, предоставив единообразный интерфейс.

REpresentational State Transfer — «передача репрезентативного состояния» или «передача „самоописываемого“ состояния»

  
  

Он предоставляет принципы, которые определяют взаимодействие между клиентом и сервером.

  

## Пример ресурсного роутинга:

(маршрутизация запросов к ресурсам (например, данным или услугам) на веб-сервере. )

  

1. GET /articles/ — возвращает все статьи
    
2. GET /articles/new — форма для создания новой статьи
    
3. POST /articles/ — создаёт новую статью
    
4. GET /articles/1 — возвращает статью с идентификатором «1»
    
5. GET /articles/1/edit — форма редактирования статьи
    
6. PATCH или PUT /articles/1 — обновляет статью с идентификатором «1»
    
7. DELETE /articles/1 — удаляет статью с идентификатором «1»
    

  

## Преимущества REST-сервисов:

  

Простота и Легкость Понимания: REST основан на простых и понятных принципах, что делает его легким для понимания и использования.

  

Масштабируемость: RESTful сервисы обеспечивают хорошую масштабируемость. Из-за отсутствия состояния (statelessness) и единообразия интерфейса (uniform interface), их проще масштабировать по мере роста запросов.

  

Гибкость и Независимость: Клиенты и серверы могут развиваться независимо друг от друга. Изменения в сервере не обязательно влияют на клиентов и наоборот.

  

Кэширование: Возможность кэширования ресурсов улучшает производительность и снижает нагрузку на сервер.

  

Поддержка Различных Форматов Данных: REST поддерживает различные форматы представления данных, такие как JSON, XML, HTML, что обеспечивает гибкость при передаче информации.

  
  
  
  
  

## Недостатки REST-сервисов:

  

Ограниченные Возможности для Сложных Операций: В некоторых случаях, особенно когда требуются сложные операции или транзакции, REST может быть не так эффективен, как, например, [SOAP](https://habr.com/ru/articles/483204/).

  

Отсутствие Стандартов для Открытия Сервисов: REST не предоставляет строгих стандартов для описания и открытия сервисов, что может затруднить обнаружение и взаимодействие с ними.

  

Безопасность: REST не обеспечивает встроенных механизмов безопасности, и его реализация требует дополнительных мер для обеспечения защиты данных.

  

Неоднозначность в Определении Ресурсов: Иногда может возникнуть неоднозначность в определении ресурсов и методов, особенно в больших и сложных системах.

  

Неудобство при Работе с Большими Объемами Данных: В случае передачи больших объемов данных, REST может столкнуться с ограничениями производительности.

  

В целом, REST является широко используемым и эффективным стилем архитектуры для построения веб-сервисов, и его преимущества часто перевешивают недостатки, особенно в сценариях с простыми запросами и высокой масштабируемостью.

  
  
  

## Принципы REST 

В архитектуре REST (Representational State Transfer) предусмотрены шесть основных требований к проектированию API. Вот краткое описание каждого из них:

  

Клиент-серверная модель (client-server model): Разделение системы на клиентов и сервера, что позволяет им развиваться независимо друг от друга. Клиенты не зависят от внутренней реализации сервера, и наоборот.

  

Отсутствие состояния (statelessness): Каждый запрос от клиента к серверу должен содержать всю необходимую информацию для понимания и обработки запроса. Сервер не хранит состояние клиента между запросами.

  

Кэширование (cacheability): Сервер или клиент могут кэшировать ресурсы для улучшения производительности. Клиент может использовать кэш для избежания повторных запросов к серверу.

  

Единообразие интерфейса (uniform interface): Интерфейс должен быть единообразным для упрощения взаимодействия между клиентом и сервером. Это требование включает в себя использование ресурсов, уникальных идентификаторов для доступа к ресурсам, манипуляции ресурсами через представление и самопонятные сообщения.

  

Многоуровневая система (layered system): Система может быть построена в виде многоуровневой архитектуры, где каждый уровень выполняет определенные функции. Это позволяет улучшить масштабируемость и обеспечить надежность.

  

Код по требованию (code on demand): Этот пункт является опциональным. Если клиент может выполнить код, полученный от сервера (например, в виде сценариев JavaScript), то он может загружать и выполнять его. Это предоставляет дополнительные возможности, но не является обязательным для соблюдения стандарта REST.

  

RESTful API, следующее этим требованиям, обеспечивают удобство, масштабируемость и универсальность взаимодействия между компонентами системы.

  

## Форматы данных использующиеся в REST-сервисах.

Архитектура REST позволяет поставщикам API доставлять данные в различных форматах, таких как: простой текст, HTML, XML, YAML и JSON.

  

## REST и SOAP

REST — это архитектурный стиль. SOAP — это формат обмена сообщениями.

  

1. Специфика SOAP — это формат обмена данными. С SOAP это всегда SOAP-XML, который представляет собой XML, включающий:
    

— Envelope (конверт) – корневой элемент, который определяет сообщение и пространство имен, использованное в документе,

— Header (заголовок) – содержит атрибуты сообщения, например: информация о безопасности или о сетевой маршрутизации,

— Body (тело) – содержит сообщение, которым обмениваются приложения,

— Fault – необязательный элемент, который предоставляет информацию об ошибках, которые произошли при обработке сообщений. И запрос, и ответ должны соответствовать структуре SOAP.

  

2. Специфика REST — использование HTTP в качестве транспортного протокола. Он подразумевает наилучшее использование функций, предоставляемых HTTP — методы запросов, заголовки запросов, ответы, заголовки ответов и т. д.
    

  

## ResponseBody, RequestBody, ResponseEntity

@ResponseBody, @RequestBody и ResponseEntity - это аннотации и класс в Spring Framework, используемые для работы с передачей данных между клиентом и сервером в веб-приложениях.

  

@ResponseBody:

Эта аннотация в Spring используется для указания, что возвращаемое методом значение должно быть прямо включено в тело ответа HTTP, а не интерпретироваться как имя представления для отображения. Обычно применяется к методам контроллера для возврата данных в формате JSON или других форматах.

  

@GetMapping("/getSomeData")

@ResponseBody

public String getSomeData() {

    return "Hello, World!";

}

@RequestBody:

Аннотация используется для привязки тела HTTP-запроса к объекту метода контроллера. Она принимает данные, отправленные клиентом в теле запроса, и маппит их на объект Java.

  

@PostMapping("/postData")

public ResponseEntity<String> postData(@RequestBody SomeObject someObject) {

    // Обработка данных

    return ResponseEntity.ok("Data received successfully");

}

ResponseEntity:

Это класс в Spring Framework, представляющий полный HTTP-ответ, включая статус ответа, заголовки и тело. ResponseEntity предоставляет более гибкий способ управления ответом, чем простые типы возвращаемых значений.

  

@GetMapping("/getResponseEntity")

public ResponseEntity<String> getResponseEntity() {

    HttpHeaders headers = new HttpHeaders();

    headers.add("Custom-Header", "Header-Value");

  

    return new ResponseEntity<>("Hello, World!", headers, HttpStatus.OK);

}

В приведенном примере, ResponseEntity позволяет установить заголовки ответа, статус ответа и тело ответа. Это может быть полезно, например, при необходимости передать дополнительные данные вместе с ответом.

  
  

## AJAX/fetch

AJAX (Asynchronous JavaScript and XML):

Технология для асинхронного обмена данными между клиентом и сервером.

Использует объект XMLHttpRequest для отправки асинхронных HTTP-запросов.

Позволяет обновлять содержимое веб-страницы без её полной перезагрузки.

Данные часто передаются в форматах XML, JSON.

  

fetch:

Современный API для работы с HTTP-запросами в JavaScript.

Возвращает объект Promise для обработки результатов асинхронных операций.

Более простой и гибкий по сравнению с XMLHttpRequest.

Применяется для обмена данными с сервером, обычно в формате JSON.

Удобен для обработки ошибок с использованием метода .catch()

  
  

Базовый синтаксис:

|   |
|---|
|let promise = fetch(url, [options])  <br>/*url - URL для отправки запроса.  <br>options - дополнительные параметры: метод, заголовки и так далее*/|

## RestController

@RestController – это просто сокращенная запись для @Controller + @ResponseBody.

  

@Controller используется для обозначения класса как контроллера в Spring MVC, который обрабатывает HTTP-запросы.

  

@ResponseBody указывает, что возвращаемое значение метода должно быть преобразовано в тело ответа HTTP, например, в формат JSON или XML.

  
  

## RestTemplate и его методы

RestTemplate это специальный клиент для отправки запросов в Spring. Он предоставляет методы для выполнения HTTP-запросов, обработки ответов и работы с различными форматами данных, такими как JSON или XML.

  

|   |
|---|
|RestTemplate restTemplate = new RestTemplate();  <br>String fooResourceUrl = "http://localhost:8080/spring-rest/foos";  <br>ResponseEntity response  = restTemplate.getForEntity(fooResourceUrl + "/1", String.class);|

Основные методы:

getForEntity -  выполняет запрос GET и возвращает объект ResponseEntity;

getForObject -  аналогично getForEntity, но возвращает ресурс напрямую;

exchange -  выполняет указанный метод HTTP, такой как GET, POST, PUT и т. д., и возвращает объект ResponseEntity;

execute - аналогичен exchange методу, но требует дополнительных параметров: RequestCallback и ResultSetExtractor;

headForHeaders -  выполняет запрос HEAD и возвращает все заголовки;

optionsForAllow -  выполняет запрос OPTIONS и использует заголовок Allow;

delete -  удаляет ресурсы по указанному URL-адресу с помощью метода HTTP DELETE;

put -  обновляет ресурс для заданного URL-адреса с помощью метода HTTP PUT;

postForObject -  создает новый запрос с использованием метода HTTP POST и возвращает сущность;

postForLocation -  создает новый запрос с использованием метода HTTP POST и возвращает его расположение;

  
  
  

"ресурс" - это данные из тела ответа, преобразованные в объект

Это не json а уже какой-то объект полноценный

RestTemplate уже за нас преобразует в объект

Вручную парсить JSON не нужно

Это происходит автоматически

  

# HTTP

[Простым языком об HTTP / Хабр](https://habr.com/ru/articles/215117/)

  

- ## HTTP и его методы
    

HTTP (англ. - Hyper Text Transfer Protocol) — широко распространённый протокол передачи данных, изначально предназначенный для передачи гипертекстовых документов (то есть документов, которые могут содержать ссылки, позволяющие организовать переход к другим документам).

Протокол HTTP предполагает использование клиент-серверной структуры передачи данных. Клиентское приложение формирует запрос и отправляет его на сервер, после чего серверное программное обеспечение обрабатывает данный запрос, формирует ответ и передаёт его обратно клиенту. После этого клиентское приложение может продолжить отправлять другие запросы, которые будут обработаны аналогичным образом.

Задача, которая традиционно решается с помощью протокола HTTP — обмен данными между пользовательским приложением, осуществляющим доступ к веб-ресурсам (обычно это веб-браузер) и веб-сервером. На данный момент именно благодаря протоколу HTTP обеспечивается работа Всемирной паутины.

  

GET

Метод GET запрашивает представление ресурса. Запросы с использованием этого метода могут только извлекать данные.

HEAD

Запрашивает ресурс так же, как и метод GET, но без тела ответа.

POST

Используется для отправки сущностей к определенному ресурсу. Часто вызывает изменение состояния или какие-то побочные эффекты на сервере.

PUT

Заменяет все текущие представления ресурса данными запроса.

DELETE

Удаляет указанный ресурс.

  
  
  
  
  

## Как устроен http запрос?

  

HTTP (Hypertext Transfer Protocol) запрос состоит из нескольких компонентов, каждый из которых выполняет определенную функцию. Вот основные компоненты структуры HTTP-запроса:

  

Строка запроса (Request Line):

Метод запроса (GET, POST, PUT, DELETE и др.).

URI (Uniform Resource Identifier) - указывает на ресурс, который нужно обработать.

Версия протокола HTTP (например, HTTP/1.1).

Пример:

GET /example/resource HTTP/1.1

  

Заголовки (Headers):

Заголовки предоставляют метаданные о запросе, такие как тип контента, язык, информация об авторизации и другие.

Каждый заголовок представляется в виде строки "Имя: Значение".

Пример:

Host: www.example.com

User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.212 Safari/537.36

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8

  

Тело запроса (Body):

Необязательная часть запроса, используемая для передачи данных, например, при отправке формы или JSON-данных.

В случае GET-запроса тело обычно отсутствует.

Пример:

username=johndoe&password=secret

  

Итак, полный HTTP-запрос может выглядеть примерно так:

GET /example/resource HTTP/1.1

Host: www.example.com

User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.212 Safari/537.36

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8

  

Важно отметить, что HTTP-запросы могут различаться в зависимости от метода, используемого в запросе, и цели запроса.

  

- ## Идемпотентность HTTP-методов
    

Метод считается «идемпотентным», если эффект на сервер от одного запроса такой же как от нескольких идентичных запросов такого типа. PUT, DELETE и безопасные методы (только на чтение — не изменяют состояние сервера) запросы являются идемпотентными.

Другими словами если многократное повторение одних и тех же запросов возвращает одинаковые результаты, то метод считается идемпотентным.

Идемпотентный и небезопасный — значит, что, сколько бы ни повторялся запрос, только первый изменит состояние системы, а остальные состояние системы не меняют.

Идемпотентный и безопасный — многократное повторение запроса вернет одно и то же состояние системы (если ресурс не изменился между ними по иным причинам).

Из спецификации HTTP:

  

|   |   |   |   |
|---|---|---|---|
|Метод|Безопасный|Идемпотентный|Ссылка|
|CONNECT|нет|нет|[Section 4.3.6](https://tools.ietf.org/html/rfc7231#section-4.3.6)|
|DELETE|нет|да|[Section 4.3.5](https://tools.ietf.org/html/rfc7231#section-4.3.5)|
|GET|да|да|[Section 4.3.1](https://tools.ietf.org/html/rfc7231#section-4.3.1)|
|HEAD|да|да|[Section 4.3.2](https://tools.ietf.org/html/rfc7231#section-4.3.2)|
|OPTIONS|да|да|[Section 4.3.7](https://tools.ietf.org/html/rfc7231#section-4.3.7)|
|POST|нет|нет|[Section 4.3.3](https://tools.ietf.org/html/rfc7231#section-4.3.3)|
|PUT|нет|да|[Section 4.3.4](https://tools.ietf.org/html/rfc7231#section-4.3.4)|
|TRACE|да|да|[Section 4.3.8](https://tools.ietf.org/html/rfc7231#section-4.3.8)|

  

GET: Это безопасный и идемпотентный метод. Он используется только для получения информации и не вносит изменений на сервере.

HEAD: Аналогично методу GET, но без передачи тела ответа. Также безопасный и идемпотентный.

PUT: Идемпотентный метод, который используется для обновления или создания ресурса по определенному URI. Многократное повторение запроса PUT с одними и теми же данными не должно изменять состояние сервера.

DELETE: Идемпотентный метод для удаления ресурса. Повторные запросы на удаление одного и того же ресурса не должны изменять состояние сервера после первого успешного запроса.

POST: Небезопасный и неидемпотентный метод. Обычно используется для создания новых ресурсов. Повторные запросы с теми же данными могут привести к созданию дополнительных ресурсов.

PATCH: Неидемпотентный метод, который используется для частичного обновления ресурса. Повторные запросы могут привести к различным состояниям, в зависимости от предыдущих изменений.

  

## HTTP-заголовки 

HTTP Headers - это строки в HTTP-сообщении, содержащие разделенную двоеточием пару параметр-значение.

Заголовки должны отделяться от тела сообщения хотя бы одной пустой строкой.

Пример:

Server: Apache/2.2.11 (Win32) PHP/5.3.0

Last-Midified: Sat, 16 Jan 2010 21:16:42 GMT

Content-Type: text/plain; charset=windows-1251

Content-Language: ru

  

Заголовки играют ключевую роль в протоколе HTTP, обеспечивая передачу дополнительной информации и управление поведением клиентов и серверов.

  
  
  
  
  

## HTTP-сессия

Это диалоговое состояние между клиентом и сервером, включающее информацию о предыдущих запросах клиента и ответах сервера.

Так как HTTP — это клиент-серверный протокол, HTTP сессия состоит из трёх фаз:

1. Клиент устанавливает TCP соединения (или другое соединение, если не используется TCP транспорт).
    

  

2. Клиент отправляет запрос и ждёт ответа.
    

  

3. Сервер обрабатывает запрос и посылает ответ, в котором содержится код статуса и соответствующие данные.
    

  
  

Начиная с версии HTTP/1.1, после третьей фазы соединение не закрывается, так как клиенту позволяется инициировать другой запрос. То есть, вторая и третья фазы могут повторяться.

  

TCP (Transmission Control Protocol) - это протокол транспортного уровня, предназначенный для обеспечения надежного и упорядоченного доставления данных между устройствами в сети. TCP работает поверх протокола IP (Internet Protocol) и часто совместно с ним обозначается как TCP/IP.

  

- ## Коды состояний HTTP
    

1xx (Информационное): Эти коды предоставляют только информацию и обычно не вызывают завершения запроса. Пример: 100 Continue (продолжение). CONTINUE

  

2xx (Успешно): Эти коды указывают на успешное выполнение запроса. Пример: 200 OK (успешно).

  

3xx (Редирект): Эти коды информируют клиента о том, что ему необходимо выполнить дополнительные действия для завершения запроса. Пример: 302 Found (найдено, редирект).

  

4xx (Ошибка клиента): Эти коды указывают на ошибку со стороны клиента. Пример: 404 Not Found (не найдено).

  

5xx (Ошибка сервера): Эти коды указывают на ошибку со стороны сервера. Пример: 500 Internal Server Error (внутренняя ошибка сервера).

  
  

# Дополнительные вопросы

- ## SpringBoot и SpringMVC
    

Прежде всего, это две разные технологии, и задачи, которые они решают, разные.

Spring MVC - это фреймворк, основанный на сервлетах. Он решает проблему разработки Web-сервисов с помощью Dispatcher Servlet и ModelAndView. Его конфигурация громоздка, с большим количеством файлов .xml и .properties, а при использовании сборщика проектов maven легко возникают конфликты пакетов jar.

Spring Boot - это пакет для быстрой разработки и интеграции на основе Spring, который включает не только Spring MVC, но также Spring JPA и Spring Security. Призван реализовать автоматическую настройку и снизить сложность построения проекта. А встроенный сервер Tomcat упрощает запуск и решает проблему конфликтов пакетов jar. Транзитивных зависимостей находятся в стартере.

  

- ## @PathVariable и @RequestParam
    

Это аннотации в Spring Framework, используемые для извлечения параметров из URI запроса.

@RequestParam используется для доступа к значениям параметров из запроса.

Используется для извлечения параметров из строки запроса (query string) после знака вопроса в URI.

Применяется, когда значения параметров передаются в URI как пары "ключ-значение" в query string, например, /users?id=123.

Пример использования:

  

|   |
|---|
|/*http://localhost:8080/springmvc/hello/101?param1=10&param2=20  <br>*/  <br>public String getDetails(@RequestParam(value="param1",required=true) String param1, @RequestParam(value="param2", required=false) String param2){  <br>...  <br>}|

  
  
  
  
  
  
  
  

@PathVariable определяет шаблон, который используется в URI входящего запроса.

Используется для извлечения переменных из шаблона URI (часть пути после слэша).

Применяется, когда значения параметров передаются в URI к’[[ часть пути, например, /users/{userId}.

  

|   |
|---|
|/*http://localhost:8080/springmvc/hello/101?param1=10&param2=20*/  <br>@RequestMapping("/hello/{id}")    <br><br>public String getDetails(@PathVariable(value="id")String id,  <br>@RequestParam(value="param1", required=true)String param1,  <br>@RequestParam(value="param2", required=false)String param2){  <br>.......  <br>}|

- ## Определение реактивных потоков данных (не надо знать)
    

Reactive Streams – это инициатива, запущенная в конце 2013 года инженерами из Netflix, Lightbend и Pivotal (последняя компания в этом списке как раз и занимается разработкой Spring). Цель Reactive Streams – поддержка стандарта асинхронной обработки потоков с неблокирующим обратным давлением (backpressure).

Это позволяет выполнять задачи параллельно и достигать большей масштабируемости. Обратное давление – это средство, помогающее получателям данных избежать перегрузки при работе со слишком быстрым источником данных; с его помощью получатели могут установить ограничение на объем, который они готовы обработать в единицу времени.

Спецификацию Reactive Streams можно свести к четырем определениям интерфейсов: Publisher, Subscriber, Subscription и Processor.

Издатель Publisher создает данные и отправляет их подписчику Subscriber. Интерфейс издателя Publisher объявляет единственный метод subscribe(), с помощью которого подписчик Subscriber может подписаться на события издателя. После оформления подписки подписчик Subscriber может получать события от издателя. Эти события отправляются через методы в интерфейсе подписчика Subscriber.

Первое событие, которое получит подписчик, – это вызов onSubscribe(). Когда издатель вызывает onSubscribe(), он передает объект Subscription подписчику. Именно через Subscription подписчик Subscribe может управлять своей подпиской. 

После запроса данных подписчиком Subscriber они начинают передаваться через поток.

Так же как подписчик Subscriber, процессор Processor будет получать и каким-то образом обрабатывать данные. Затем он сменит ориентацию и будет действовать как издатель Publisher, чтобы опубликовать новые данные для своих подписчиков.

Следует упомянуть также об основных типах, реализующих интерфейс Publisher: Mono и Flux. Тип Flux представляет конвейер из произвольного количества (от нуля до бесконечности) элементов данных. Mono – это специализированный реактивный тип, оптимизированный для случаев, когда известно, что набор данных содержит не более одного элемента данных.

- ## RestTemplate vs WebClient (WebClient - часть реактивного программирования курса JavaAdvanced)
    

RestTemplate появился еще в версии Spring 3.0. В свое время он использовался для выполнения запросов от имени приложений, которые его используют.

Но все методы RestTemplate работают с нереактивными прикладными типами и коллекциями. 

Spring предлагает WebClient – реактивную альтернативу RestTemplate. WebClient позволяет отправлять и получать реактивные типы при работе с внешними API. 

Использование WebClient сильно отличается от использования RestTemplate. Вместо нескольких методов для работы с разными типами запросов WebClient предлагает гибкий интерфейс в стиле конструктора, который позволяет описывать и отправлять запросы. Вот как выглядит общий алгоритм работы с WebClient:

1. создать экземпляр WebClient (или внедрить компонент WebClient);
    
2. указать HTTP-метод отправляемого запроса;
    
3. указать URI и любые заголовки, которые должны быть в запросе;
    
4. отправить запрос;
    
5. получить и использовать ответ.
    

|   |
|---|
|Mono<Ingredient> ingredient = WebClient.create()  <br>.get()  <br>.uri("http://localhost:8080/ingredients/{id}", ingredientId)  <br>.retrieve()  <br>.bodyToMono(Ingredient.class);  <br>ingredient.subscribe(i -> { ... });|

  
  
**